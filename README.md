# 🍀 Loterial Pro — Central de Inteligência Cloud & Apostas Múltiplas

O **Loterial Pro** é uma plataforma comercial de alto desempenho voltada para análise estatística, desdobramentos matemáticos e fechamentos combinatórios customizados para a Lotofácil. O sistema permite a geração de cartões que vão desde a **aposta simples (15 dezenas) até apostas múltiplas avançadas (16, 17 e 18 dezenas)**, integrando-se diretamente à nuvem do **Google Firebase** para sincronização de dados e gerenciamento de licenças.

---

## 🚀 Principais Funcionalidades

* **Suporte Completo a Apostas Múltiplas (15 a 18 Dezenas):** * Permite ao usuário expandir o tamanho do bilhete gerado.
  * O sistema calcula automaticamente o custo proporcional real de cartões maiores baseado nos critérios da Caixa Econômica Federal.
* **7 Motores Combinatórios Avançados:** * *Matriz Personalizada:* Definição manual de 5 dezenas Fixas e 12 Semi-Fixas.
  * *Filtro Geométrico:* Distribuição inteligente entre Moldura (Borda) e Miolo (Centro).
  * *Equilíbrio Linear:* Geração distribuída com travas automáticas por quadrantes.
  * *Desdobramentos R4, R5 e R6:* Fechamentos focados em eliminação estratégica de dezenas (elimine 4, 5 ou 6 números) com garantia matemática.
  * *Estratégia ABC de Grupos:* Segregação automatizada em dezenas Repetidas (Grupo A), Quentes (Grupo B) e Frias (Grupo C).
  * *Fechamento de Ciclo:* Travas baseadas no comportamento de dezenas mais atrasadas na nuvem.
* **Módulo de Conferência Avançada com Desdobramento de Prêmios:** * O conferidor detecta o tamanho de cada bilhete enviado (15 a 18 números) e desdobra as premiações automaticamente. Se um bilhete de 16 dezenas obtiver 13 acertos diretos, o sistema calcula e exibe o pagamento equivalente oficial: **3 prêmios de 13 acertos + 13 prêmios de 12 acertos**.
* **Balanço Financeiro Automatizado:** Relatórios em tempo real contendo o Custo Total Múltiplo do grupo, o faturamento bruto em Prêmios Desdobrados e o Saldo Líquido (lucro/prejuízo).
* **Filtro Antiduplicidade:** Trava de segurança no banco de dados NoSQL que impede o cadastro por engano do mesmo concurso mais de uma vez.
* **Guia Interativo Embutido:** Central de ajuda flutuante (Modal) acessível com um clique direto no cabeçalho.

---

## 🔒 Camada Comercial e Segurança (Firebase Auth + Firestore Rules)

O projeto foi estruturado para distribuição comercial de software como serviço (SaaS). A segurança é gerenciada diretamente no servidor da Google por meio de **Firestore Security Rules**, tornando o código-fonte imune a tentativas de manipulação ou burlas locais:

1.  **Bloqueio por Licença:** Ao se cadastrar, o cliente entra automaticamente no status `Pendente`. O acesso aos motores de geração e ao histórico em nuvem só é liberado após o administrador alterar o status para `Ativo` no painel.
2.  **Painel Administrativo Oculto:** O aplicativo detecta perfis administrativos diretamente pelas permissões de leitura do servidor, renderizando uma aba exclusiva para ativação e bloqueio de clientes em tempo real, sem expor chaves ou e-mails no código-fonte.

---

## 🛠️ Tecnologias Utilizadas

* **Frontend:** HTML5 estrutural, CSS3 (Variáveis nativas, animações de interface e design responsivo focado em dispositivos móveis).
* **Lógica:** JavaScript Puro (ES6+) assíncrono e modular.
* **Backend & Infraestrutura:** * *Firebase Authentication:* Gerenciamento seguro de credenciais de usuários.
  * *Cloud Firestore:* Banco de dados NoSQL para persistência de concursos e controle de licenças.

---

## 📦 Como Executar o Projeto Localmente

Por ser um sistema construído em arquivo único estruturado, ele não exige a instalação de gerenciadores de pacotes pesados (como o Node.js) para rodar em modo de produção do cliente:

1. Clone este repositório:
   ```bash
   git clone [https://github.com/seu-usuario/loterial-pro.git](https://github.com/seu-usuario/loterial-pro.git)
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
