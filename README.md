```markdown
# 🍀 Loterial Pro — Central de Inteligência Cloud

O **Loterial Pro** é uma plataforma comercial voltada para análise estatística, desdobramentos matemáticos e fechamentos combinatórios customizados para a Lotofácil. Desenvolvido com uma arquitetura *offline-first* moderna, o sistema integra-se diretamente à nuvem do **Google Firebase** para oferecer sincronização de dados entre grupos e gerenciamento comercial de licenças de acesso.

---

## 🚀 Principais Funcionalidades

* **6 Motores Combinatórios Avançados:** * *Matriz Personalizada:* Definição manual de 5 dezenas Fixas e 12 Semi-Fixas.
    * *Filtro Geométrico:* Distribuição inteligente baseada em comportamento de Moldura (Borda) vs. Miolo (Centro).
    * *Equilíbrio Linear:* Geração distribuída com travas por quadrantes (3 dezenas por linha).
    * *Desdobramentos R5 e R6:* Fechamentos focados em exclusão de dezenas com garantia matemática.
    * *Estratégia ABC de Grupos:* Análise automática segregando dezenas em Repetidas (Grupo A), Quentes (Grupo B) e Frias (Grupo C).
    * *Fechamento de Ciclo:* Travas de segurança baseadas nas dezenas mais atrasadas da nuvem.
* **Mapa de Calor em Tempo Real:** Análise visual cumulativa de frequência que indica quais dezenas estão *Quentes* ou *Frias* com base no histórico global do servidor.
* **Conferidor em Grupo & Painel Financeiro:** Módulo de cruzamento de bilhetes em lote com cálculo instantâneo de custo de apostas, totalização de prêmios e saldo líquido do grupo.
* **Filtro Antiduplicidade:** Banco de dados inteligente que impede o cadastro acidental de concursos repetidos.
* **Guia Interativo Embutido:** Central de ajuda simplificada integrada na interface para orientação ao usuário.

---

## 🔒 Camada Comercial e Segurança (Firebase Auth + Firestore Rules)

O projeto foi estruturado para distribuição comercial de software como serviço (SaaS). A segurança é gerenciada diretamente no servidor da Google por meio de **Firestore Security Rules**, tornando o código do repositório imune a adulterações locais:

1.  **Bloqueio por Licença:** Ao se cadastrar, o cliente entra automaticamente no status `Pendente`. O acesso aos motores de geração e ao histórico em nuvem só é liberado após o administrador alterar o status para `Ativo` no painel.
2.  **Painel Administrativo Oculto:** O aplicativo detecta perfis administrativos diretamente pelas permissões do servidor, renderizando uma aba exclusiva para ativação e bloqueio de clientes em tempo real, sem expor chaves ou e-mails no código-fonte.

---

## 🛠️ Tecnologias Utilizadas

* **Frontend:** HTML5 estrutural, CSS3 (Variáveis nativas, animações de interface e design responsivo focado em dispositivos móveis).
* **Lógica:** JavaScript Puro (ES6+) assíncrono.
* **Backend & Infraestrutura:** * *Firebase Authentication:* Gerenciamento seguro de credenciais de usuários.
    * *Cloud Firestore:* Banco de dados NoSQL para persistência de concursos e controle de licenças.

---

## 📦 Como Executar o Projeto Localmente

Por ser um sistema construído em arquivo único estruturado, ele não exige a instalação de gerenciadores de pacotes pesados como o Node.js para rodar em modo de produção do cliente:

1. Clone este repositório:
   ```bash
   git clone [https://github.com/seu-usuario/loterial-pro.git](https://github.com/seu-usuario/loterial-pro.git)

```

2. Abra o arquivo `index.html` em qualquer navegador ou utilize a extensão *Live Server* do VS Code / Bloco de Notas Avançado.

---

## 💳 Fluxo de Aquisição e Liberação de Acesso

Se você deseja contratar ou renovar sua licença de uso da plataforma:

1. Acesse a aplicação e clique na aba **"Criar Conta"**.
2. Efetue o registro informando seu e-mail e uma senha de preferência.
3. Realize o pagamento da sua taxa de licença via **Pix** para o proprietário do software.
4. **Envie o comprovante de pagamento** imediatamente ao administrador para que sua conta seja alterada de `Pendente` para `Ativo` no painel central.

---

## 📄 Licença

Este software é disponibilizado para uso comercial sob licença proprietária. É proibida a redistribuição, engenharia reversa ou cópia não autorizada deste código-fonte sem o consentimento expresso do desenvolvedor.
