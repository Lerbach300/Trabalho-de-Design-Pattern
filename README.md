//AULA 7 SIGLETON

class Mcinfeliz{
    private static Mcinfeliz instance;
    private String nome;
    private String endereco;

    // Construtor privado para impedir a criação de instâncias fora da classe
    private Mcinfeliz(String nome, String endereco) {
        this.nome = nome;
        this.endereco = endereco;
    }

    // Método estático para obter a instância única da empresa
    public static Mcinfeliz getInstance() {
        if (instance == null) {
            instance = new Mcinfeliz("McLanche Infeliz", "Rua dos Burgâo, 567");
        }
        return instance;
    }

    // Métodos para acessar informações da empresa
    public String getNome() {
        return nome;
    }

    public String getEndereco() {
        return endereco;
    }
}

public class Main {
    public static void main(String[] args) {
        // Obtendo a instância da empresa
       Mcinfeliz mcinfeliz = Mcinfeliz.getInstance();

        // Acessando informações da empresa
        System.out.println("Nome: " + mcinfeliz.getNome());
        System.out.println("Endereço: " + mcinfeliz.getEndereco());

        // Tentando criar outra instância da empresa - retornará a mesma instância
        Mcinfeliz anotherInstance =mcinfeliz.getInstance();
        System.out.println("As duas instâncias são iguais? " + (mcinfeliz == anotherInstance)); // Deve imprimir true
    }
}

//AULA 8 COMPOSITE

public class Main {
    public static void main(String[] args) {
       
        Ingrediente pao = new Pao();
        Ingrediente hamburguer = new Hamburguer();
        Ingrediente queijo = new Queijo();
        Ingrediente alface = new Alface();
        Ingrediente tomate = new Tomate();
        Ingrediente molho = new Molho();
    
        JuntarIngredientes juntar = new JuntarIngredientes();
        juntar.add(pao);
        juntar.add(hamburguer);
        juntar.add(queijo);
        juntar.add(alface);
        juntar.add(tomate);
        juntar.add(molho);
       
       
       
       
       
        juntar.adicionar();
    }
}


interface Ingrediente {
    void adicionar();
}


class Pao implements Ingrediente {
    @Override
    public void adicionar() {
        System.out.println("Adicionando pão.");
    }
}


class Hamburguer implements Ingrediente {
    @Override
    public void adicionar() {
        System.out.println("Adicionando hamburguer.");
    }
}

class Queijo implements Ingrediente {
    @Override
    public void adicionar() {
        System.out.println("Adicionando queijo.");
    }
}

class Alface implements Ingrediente {
    @Override
    public void adicionar() {
        System.out.println("Adicionando alface.");
    }
}

class Tomate implements Ingrediente {
    @Override
    public void adicionar() {
        System.out.println("Adicionando tomate.");
    }
}

class Molho implements Ingrediente {
    @Override
    public void adicionar() {
        System.out.println("Adicionando molho.");
    }
}


import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

// Composição (parte composta)
class JuntarIngredientes implements Ingrediente {
    private final List<Ingrediente> sanduiche = new ArrayList<>();

    void add(Ingrediente ingrediente) {
        sanduiche.add(ingrediente);
    }

    void remove(Ingrediente ingrediente) {
        sanduiche.remove(ingrediente);
    }

    @Override
    public void adicionar() {
        for (Ingrediente ingrediente : sanduiche) {
            ingrediente.adicionar();
        }
    }
}

//AULA 9 COMMAND

public class Main {
    public static void main(String[] args) {
        Caixa caixa = new Caixa();

        Comando lanche = new VendeLanche();
        Comando batata = new VendeBatata();
        Comando refri = new VendeRefri();

        caixa.setComando(lanche);
        caixa.pressionarBotao();

        caixa.setComando(batata);
        caixa.pressionarBotao();
        
        caixa.setComando(refri);
        caixa.pressionarBotao();
    }
}

class Caixa {
    private Comando comando;

    public void setComando(Comando comando) {
        this.comando = comando;
    }

    public void pressionarBotao() {
        comando.executar();
    }
}

class VendeLanche implements Comando {
    public void executar() {
        System.out.println("Lanche vendido");
    }
}

class VendeBatata implements Comando {
    public void executar() {
        System.out.println("Batata vendida");
    }
}

class VendeRefri implements Comando {
    public void executar() {
        System.out.println("Refrigerante vendido");
    }
}

interface Comando {
    void executar();
}
