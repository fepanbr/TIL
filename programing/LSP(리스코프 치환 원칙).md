#### LSP(리스코프 치환 원칙)

자식형을 부모형으로 안전하게 대체할 수 있다.



> 묻지마!! 그건 계속 변해. 자기상태는 자기가 관리해. 그러니까 **시켜!!!** 그건 할지 안할지는 걔가 알아서 할거야.



주제 : 구상층이 늘어나는 문제는 **제네릭**으로 해결한다.



```java
public interface Paper {}

public interface Programmer {
    Program makeProgram(Paper paper);
}
```



```java
public interface Paper{}

public class Client implements Paper {
    Library library = new Library("vueJS");
    Language language = new Library("kotlinJS");
    
}
```



```java
public interface Programmer {
    Program makeProgram(Paper paper);
}
public class FrontEnd implements Programmer{
    private Language language;
    private Library library;
    @Override
    public Program makeProgram(Paper paper) {
        if(paper instanceof Client) {
            Client pb = (Client)paper;
            language = pb.language;
            library = pb.library;
        }
        return makeFrontEndProgram();
    }
    private Program makeFrontEndProgram(){return new Program();}
}

public class BackEnd implements Programmer{
    private Language language;
    private Library library;
    @Override
    public Program makeProgram(Paper paper) {
        if(paper instanceof ServerClient) {
            ServerClient pb = (ServerClient)paper;
            language = pb.language;
            library = pb.library;
        }
        return makeFrontEndProgram();
    }
    private Program makeFrontEndProgram(){return new Program();}
}
```



````java
public class Director {
    private Map<String, Paper> projects = new HashMap<>();
    public void addProject(String name, Paper paper){projects.put(name, paper);}
    public void runProject(String name) {
        if(!project.containsKey(name)) throw new RuntimeExecption("no Project");
        Paper paper = projects.get(name);
        if(paper instanceof ServerClient) {
            ServerClient project = (ServerClient)paper;
            Programmer fronEnd = new FrontEnd(), backEnd = new BackEnd();
            project.setFrontEndProgrammer(fronEnd);
            project.setBackEndProgrammer(backEnd);
            Program client = fronEnd.makeProgram(project);
            Program server = backEnd.makeProgram(project);
            deploy(name, client, server); 
            
        } else if (paper instanceof Client) {
            Client project = (Client)paper;
            Programmer fronEnd = new FrontEnd();
            project.setFrontEndProgrammer(fronEnd);
            deploy(name, frontEnd.makeProgram(project));
        }
    }
    private void deploy(String projectName, Program...programs){}
}
````



잘못된 frontEnd 클래스 변경

```java
public class FrontEnd implements Programmer{
    private Language language;
    private Library library;
    @Override
    public Program makeProgram(Paper paper) {
        paper.setData(this);
        return makeFrontEndProgram();
    }
    void setLanguage(Language language){this.language = language;}
    void setLibrary(Library library){this.library = library;}
    private Program makeFrontEndProgram(){return new Program();}
}
```



Paper

```java
public interface Paper {
    void setData(Programmer programmer);
}

public class Client implements Paper {
    Library library = new Library("vueJS");
    Language language = new Language("kotlinJS");
    Programmer programmer;
    public void setProgrammer(Programmer programmer) {
        this.programmer = programmer;
    }
    @Override
    public void setData(Programmer programmer) {
        if(programmer instanceof FrontEnd) {
            FrontEnd fronEnd = (FrontEnd)programmer;
            frontEnd.setLibrary(library);
            frontEnd.setLanguage(language);
        }
        // 문제가 있다. 결국 LSP는 해결되지 않는다.
    }
}
```

