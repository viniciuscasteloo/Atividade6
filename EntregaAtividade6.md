import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

interface Notificacao {
    void enviar(String mensagem);
}

class NotificacaoEmail implements Notificacao {
    @Override
    public void enviar(String mensagem) {
        System.out.println("Enviando e-mail: " + mensagem);
    }
}

class NotificacaoSms implements Notificacao {
    @Override
    public void enviar(String mensagem) {
        System.out.println("Enviando SMS: " + mensagem);
    }
}

class NotificacaoWhatsApp implements Notificacao {
    @Override
    public void enviar(String mensagem) {
        System.out.println("Enviando WhatsApp: " + mensagem);
    }
}

class ServicoNotificacao {
    public void notificarCliente(Notificacao notificacao, String mensagem) {
        notificacao.enviar(mensagem);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        List<Notificacao> notificacoes = new ArrayList<>();
        notificacoes.add(new NotificacaoEmail());
        notificacoes.add(new NotificacaoSms());
        notificacoes.add(new NotificacaoWhatsApp());

        ServicoNotificacao servico = new ServicoNotificacao();

        System.out.println("=== Sistema de Notificações ===");
        System.out.println("Escolha o tipo de notificação:");
        System.out.println("1 - E-mail 📧");
        System.out.println("2 - SMS 📱");
        System.out.println("3 - WhatsApp 💬");
        System.out.print("Opção: ");

        int opcao = scanner.nextInt();
        scanner.nextLine();

        if (opcao < 1 || opcao > 3) {
            System.out.println("Opção inválida. Encerrando.");
            scanner.close();
            return;
        }

        System.out.print("Digite a mensagem: ");
        String mensagem = scanner.nextLine();

        servico.notificarCliente(notificacoes.get(opcao - 1), mensagem);

        scanner.close();
    }
}
