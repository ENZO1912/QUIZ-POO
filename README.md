import java.io.File;
import java.util.Scanner;

public class Main {

  public static void main(String[] args) {

    Scanner t = new Scanner(System.in);

    String[][] p = new String[50][5];
    int total = 0;
    int pontos = 0; //pontuação

    try {
      Scanner arq = new Scanner(new File("Perguntas_e_Respostas.csv"));

      while (arq.hasNextLine()) {
        String[] x = arq.nextLine().split("\\|");

        for (int i = 0; i < 5; i++) {
          p[total][i] = x[i];
        }

        total++;
      }

    } catch (Exception e) {
      System.out.println("Erro arquivo");
      return;
    }

    //perguntas usadas
    boolean[] usada = new boolean[total];

    //5 perguntas
    for (int i = 0; i < 5; i++) {

      int pos;

      //sorteia uma pergunta e veriifica se foi usada
      do {
        pos = (int) (Math.random() * total);
      } while (usada[pos]);

      usada[pos] = true;

      System.out.println("\n" + p[pos][0]);

      String[] r = new String[4];

      //respostas
      for (int j = 0; j < 4; j++) {
        r[j] = p[pos][j + 1];
      }

      // embaralhar
      for (int j = 0; j < 4; j++) {
        int t2 = (int) (Math.random() * 4);

        String temp = r[j];
        r[j] = r[t2];
        r[t2] = temp;
      }
//opcpes
      System.out.println("1 - " + r[0]);
      System.out.println("2 - " + r[1]);
      System.out.println("3 - " + r[2]);
      System.out.println("4 - " + r[3]);

      int resp;

      //verifica se e a resposta e de 1 a 4
      do {
        System.out.print("Resposta (1 a 4): ");
        resp = t.nextInt();
      } while (resp < 1 || resp > 4);

      //compara a resposta
      if (r[resp - 1].equals(p[pos][1])) {
        System.out.println("Acertou");
        pontos++; // soma ponto
      } else {
        System.out.println("Errou");
      }
    }

    System.out.println("\nPontuação final: " + pontos + "/5");
  }
}
