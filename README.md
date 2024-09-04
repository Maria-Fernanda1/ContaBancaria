package ContaBancaria;
	import java.util.ArrayList;
	import java.util.List;

	public class ContaBancaria {
	    private String numeroConta;
	    private String senha;
	    private double saldo;
	    private List<String> historicoTransacoes;

	    public ContaBancaria(String numeroConta, String senha, double saldo) {
	        this.numeroConta = numeroConta;
	        this.senha = senha;
	        this.saldo = saldo;
	        this.historicoTransacoes = new ArrayList<>();
	    }

	    public String getNumeroConta() {
	        return numeroConta;
	    }

	    public String getSenha() {
	        return senha;
	    }

	    public double getSaldo() {
	        return saldo;
	    }

	    public void setSaldo(double saldo) {
	        this.saldo = saldo;
	    }

	    public List<String> getHistoricoTransacoes() {
	        return historicoTransacoes;
	    }

	    public void adicionarTransacao(String transacao) {
	        if (historicoTransacoes.size() == 5) {
	            historicoTransacoes.remove(0);
	        }
	        historicoTransacoes.add(transacao);
	    }

	    public void consultarSaldo() {
	        System.out.println("Saldo atual: R$ " + saldo);
	    }

	    public boolean sacar(double valor) {
	        if (valor <= saldo) {
	            saldo -= valor;
	            adicionarTransacao("Saque: R$ " + valor);
	            return true;
	        } else {
	            System.out.println("Saldo insuficiente.");
	            return false;
	        }
	    }

	    public void depositar(double valor) {
	        saldo += valor;
	        adicionarTransacao("Depósito: R$ " + valor);
	    }

	    public void exibirHistorico() {
	        System.out.println("Histórico de Transações:");
	        for (String transacao : historicoTransacoes) {
	            System.out.println(transacao);
	        }
	    }

	    public boolean transferir(ContaBancaria contaDestino, double valor) {
	        if (valor <= saldo) {
	            saldo -= valor;
	            contaDestino.depositar(valor);
	            adicionarTransacao("Transferência enviada: R$ " + valor);
	            contaDestino.adicionarTransacao("Transferência recebida: R$ " + valor);
	            return true;
	        } else {
	            System.out.println("Saldo insuficiente para transferência.");
	            return false;
	        }
	    }
	}
