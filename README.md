# exercicio-metodos-vetores

package main;

import java.util.Scanner;

public class Questao01 {

	static Scanner scanner = new Scanner(System.in);

	static final int TOTAL_AVALIACOES = 3;
	static final String[] NOMES_AVALIACOES = { "A1", "A2", "A3" };
	static final double[] NOTA_MAX_AVALIACOES = { 30.00, 30.00, 40.00 };

	static final int TOTAL_AI = 1;
	static final String[] NOMES_AI = { "AI" };
	static final double[] NOTA_MAX_AI = { 30.00 };
	static double[] notasAI = new double[TOTAL_AI];
	
	static double[] notas = new double[TOTAL_AVALIACOES];

	/**
	 * Ler uma nota do usuário
	 * 
	 * @param mensagem O texto que aparecerá na tela
	 * @return um número double representando a nota.
	 */

	static double lerNota(String mensagem, double notaMaxima) {

		double nota = 0.0;

		do {

			System.out.printf("%s = ", mensagem);
			nota = scanner.nextDouble();

		} while (nota < 0.00 || nota > notaMaxima);

		return nota;
	}

	/**
	 * Atualiza o valor da respectiva nota do estudante
	 * 
	 * @param indiceNota um número inteiro representando o índice (posição) da nota
	 *                   no vetor
	 */
	static void atualizarNota(int indiceNota) {

		System.out.println();
		notas[indiceNota] = lerNota(NOMES_AVALIACOES[indiceNota], NOTA_MAX_AVALIACOES[indiceNota]);

	} // Fim do método atualizarNota

	/**
	 * @param notaFinal A soma de todas as avalições feita pelo estudante ao longo
	 *                  do semestre
	 * @return uma string representando o status final do estudante, são eles:
	 *         APROVADO, REPROVADO, EM RECUPERAÇÃO.
	 */
	
	static String avaliarSituacao(double notaFinal) {

		if (notaFinal < 30)
			return "REPROVADO";
		else if (notaFinal < 70)
			return "EM RECUPERAÇÃO";
		else
			return "APROVADO";

	} // Fim do método avaliarSituacao()

	/**
	 * Mostra na tela um relatório das notas do estudante
	 */
	static void mostrarNotas() {

		double notaFinal = 0.0;

		System.out.println("\n\t\tNOTAS");
		System.out.println();

		for (int i = 0; i < TOTAL_AVALIACOES; i++) {

			System.out.printf("Avaliação %s = %.2f pts", NOMES_AVALIACOES[i], notas[i]);
			if (notas[0] > notas[1]) {
				notas[1] = notasAI[0];
				double mediaFinal;
			} else {
				System.out.println("");
			}
			System.out.println();
			notaFinal += notas[i];

		}

		System.out.printf("\nNota Final = %.2f pts", notaFinal);
		System.out.printf("\nSituação = %s\n", avaliarSituacao(notaFinal));

		double media = calcularMedia(notas);
		System.out.printf("A média final é: %.2f\n", media);

		String maior_Av = maiorNota(notas);
		System.out.println("A avaliação de maior nota foi: " + maior_Av);
		

		System.out.printf("Avaliação %s = %.2f pts", NOMES_AI[0], notasAI[0]);
		
		double mediaFinal = 0.0;
        if (notaFinal < 70) {

            if (notas[0] > notas[1]) {
                notas[1] = notasAI[0];
                mediaFinal = notas[0] + notas[1] + notas[2];
            } else {
                notas[0] = notasAI[0];
                mediaFinal = notas[0] + notas[1] + notas[2];
            }

            System.out.println("A nova nota final é: "+ mediaFinal);

            if(mediaFinal >= 70) {
                System.out.println("APROVADO");
            } else {
                System.out.println("REPROVADO");
            } 

        } else {
            System.out.println("O aluno está aprovado!");
        }

	} // Fim do método mostrarNotas()

	/**
	 * Exibe o menu principal da aplicação
	 */

	static void mostrarMenu() {

		System.out.println("\n");
		System.out.println("\t\tMENU");
		System.out.println();

		System.out.println("[1] Cadastrar Notas A1");
		System.out.println("[2] Cadastrar Nota A2");
		System.out.println("[3] Cadastrar Nota A3");
		System.out.println("[4] Cadastrar Nota da Avaliação Integral");
		System.out.println("[5] Mostrar Notas");
		System.out.println("[0] SAIR");

		System.out.print("\nDigite uma opção:  ");
		byte opcao = scanner.nextByte();

		switch (opcao) {

		case 0:
			System.exit(0);
			break;

		case 1:
			atualizarNota(0);
			break;
		case 2:
			atualizarNota(1);
			break;
		case 3:
			atualizarNota(2);
			break;
		case 4:
			atualizarNotaAI(0);
			break;
		case 5:
			mostrarNotas();
			break;
		default:
			mostrarMenu();
			break;

		}

		mostrarMenu();

	} // Fim do método mostrarMenu()

	static double calcularMedia(double[] notas) {

		double notaMedia = (notas[0] + notas[1] + notas[2]) / 3;
		return notaMedia;

	} // Fim do método calcularMedia()

	static String maiorNota(double[] notas) {

		if (notas[0] > notas[1] && notas[0] > notas[2]) {
			return "A1";
		} else if (notas[1] > notas[0] && notas[1] > notas[2]) {
			return "A2";
		} else if (notas[2] > notas[0] && notas[2] > notas[1]) {
			return "A3";
		} else if (notas[0] == notas[1] && notas[0] == notas[1] && notas[1] == notas[2]) {
			return "A1, A2 e A3";
		} else if (notas[0] == notas[2]) {
			return "A1 e A3";
		} else if (notas[1] == notas[2]) {
			return "A2 e A3";
		} else if (notas[0] == notas[1]) {
			return "A1 e A2";
		} else {
			return "Erro";
		}

	}// Fim do método maiorNota();
	
	
	static void atualizarNotaAI(int indiceAI) {
		
		System.out.println();
		notasAI[indiceAI] = lerNotaAI(NOMES_AI[indiceAI], NOTA_MAX_AI[indiceAI]);
		
	}//Fim do método atualizarNotaAI()
	
	static double lerNotaAI(String mensagem, double notaMaxima) {
		
		double nota = 0.0;
		
		do {
			System.out.printf("%s = ", mensagem);
			nota = scanner.nextDouble();
			
		} while((nota < 0) || (nota > notaMaxima));
		
		return nota;
		 
	}//Fim do método larNotaAI()

	public static void main(String[] args) {

		mostrarMenu();

	} // Fim do método main();

} // Fim da classe Main

