public class Exerciceo3  {// Árvore Binária Recursiva

    // Classe interna para representar um nó da árvore
    static class No {
        Object nome;
        No esquerda, direita;

        No(Object nome) {
            this.nome = nome;
            esquerda = direita = null;
        }
    }

    No raiz;

    private String getNome(Object objeto){
        return((Biblioteca) objeto).nome;
    }

    // Método para inserir um nome na árvore
    void inserir(Object nome) {
        raiz = inserirRecursivo(raiz, nome);
    }

    // Inserção recursiva seguindo as regras da BST
    No inserirRecursivo(No atual, Object nome) {
        if (atual == null) {
            return new No(nome);
        }
        
        String nomeNovoNo = getNome(nome);
        String nomeAtual = getNome(atual.nome);

        if (nomeNovoNo.compareToIgnoreCase(nomeAtual) < 0) {
            atual.esquerda = inserirRecursivo(atual.esquerda, nome);
        } else if (nomeNovoNo.compareToIgnoreCase(nomeAtual) > 0) {
            atual.direita = inserirRecursivo(atual.direita, nome);
        }

        return atual;
    }

    // Impressão in-order (alfabética)
    void emOrdem() {
        System.out.println("Nomes em ordem alfabética:");
        emOrdemRecursivo(raiz);
    }

    void emOrdemRecursivo(No atual) {
        if (atual != null) {
            emOrdemRecursivo(atual.esquerda);
            System.out.println(atual.nome);
            emOrdemRecursivo(atual.direita);
        }
    }
    
     // ========== NOVOS MÉTODOS DE TRAVESSIA ==========

    // Travessia em Pré-Ordem (raiz -> esquerda -> direita)
    void preOrdem() {
        System.out.println("Nomes em Pré-Ordem:");
        preOrdemRecursivo(raiz);
        System.out.println();
    }

    void preOrdemRecursivo(No atual) {
        if (atual != null) {
            System.out.print(atual.nome + " "); // 1. Visita o nó atual primeiro
            preOrdemRecursivo(atual.esquerda); // 2. Depois percorre a subárvore esquerda
            preOrdemRecursivo(atual.direita);  // 3. Por último percorre a subárvore direita
        }
    }

    // Travessia em Pós-Ordem (esquerda -> direita -> raiz)
    void posOrdem() {
        System.out.println("Nomes em Pós-Ordem:");
        posOrdemRecursivo(raiz);
        System.out.println();
    }

    void posOrdemRecursivo(No atual) {
        if (atual != null) {
            posOrdemRecursivo(atual.esquerda); // 1. Percorre a subárvore esquerda
            posOrdemRecursivo(atual.direita);  // 2. Depois percorre a subárvore direita
            System.out.print(atual.nome + " "); // 3. Exibe o nó atual por último
        }
    }

    
    // Método público para buscar um nome
    boolean buscarPorNome(String nome) {
        return buscarRecursivo(raiz, nome);
    }
    boolean buscarPorAutor(String nome) {
        return buscarRecursivo(raiz, nome);
    }
    
    // Método recursivo para busca
    boolean buscarRecursivo(No atual, String nome) {
        if (atual == null) {
            return false; // Nó não encontrado
        }
    
        String nomeAtual = getNome (atual.nome);

        if (nome.equalsIgnoreCase(nomeAtual)) {
            return true; // Nome encontrado
        }
    
        if (nome.compareToIgnoreCase(nomeAtual) < 0) {
            return buscarRecursivo(atual.esquerda, nome); // Buscar na subárvore esquerda
        } else {
            return buscarRecursivo(atual.direita, nome); // Buscar na subárvore direita
        }
    }

    public static class Biblioteca{
        public String nome, autor, ano;
        public Biblioteca(String nome, String autor, String ano){
            this.nome = nome;
            this.autor = autor;
            this.ano = ano;
        }

        @Override
        public String toString(){
            return "Livros: " + nome + " | " + autor + " | " + ano;
        }

    }

 public static void main(String[] args) {


      // ===== TESTE BIBLIOTECA =====

    Exerciceo3 arvoreBiblioteca = new Exerciceo3();

    Biblioteca[] livros = {

      new Biblioteca("Dom Casmurro", "Machado de Assis", "1899"),
      new Biblioteca("Memórias Póstumas", "Machado de Assis", "1881"),
      new Biblioteca("O Alienista", "Machado de Assis", "1882"),
      new Biblioteca("A Hora da Estrela", "Clarice Lispector", "1977"),
      new Biblioteca("Perto do Coração Selvagem", "Clarice Lispector", "1943"),
      new Biblioteca("Grande Sertão: Veredas", "Guimarães Rosa", "1956"),
      new Biblioteca("Sagarana", "Guimarães Rosa", "1946"),
      new Biblioteca("Capitães da Areia", "Jorge Amado", "1937"),
      new Biblioteca("Gabriela, Cravo e Canela", "Jorge Amado", "1958"),
      new Biblioteca("Dona Flor e Seus Dois Maridos", "Jorge Amado", "1966"),
      new Biblioteca("O Primo Basílio", "Eça de Queirós", "1878"),
      new Biblioteca("Os Maias", "Eça de Queirós", "1888"),
      new Biblioteca("A Moreninha", "Joaquim Manuel de Macedo", "1844"),
      new Biblioteca("Iracema", "José de Alencar", "1865"),
      new Biblioteca("O Guarani", "José de Alencar", "1857"),
      new Biblioteca("Senhora", "José de Alencar", "1875"),
      new Biblioteca("Vidas Secas", "Graciliano Ramos", "1938"),
      new Biblioteca("São Bernardo", "Graciliano Ramos", "1934"),
      new Biblioteca("Angústia", "Graciliano Ramos", "1936"),
      new Biblioteca("Auto da Compadecida", "Ariano Suassuna", "1955")

    };

    for (Biblioteca livro : livros) {
      arvoreBiblioteca.inserir(livro);
    }



    System.out.println("\n=== Livros na Biblioteca ===");
    arvoreBiblioteca.emOrdem();

    // Buscar livro pelo nome
    String nomeLivro = "Iracema";
    Object resultadoLivro = arvoreBiblioteca.buscarPorNome(nomeLivro);
    System.out.println("\nBusca por livro: " + resultadoLivro);

    // Buscar livros pelo autor
    String autorBusca = "Machado de Assis";
    arvoreBiblioteca.buscarPorAutor(autorBusca);

  }
}

    


    

