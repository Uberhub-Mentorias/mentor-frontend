# 📘 Requisitos Funcionais -- Mentor (UberHub)

## **RF-MTR-01 -- Cadastrar Perfil**

### **Descrição**

Permitir que o profissional crie seu perfil inicial para se candidatar
como Mentor.

### **Ator Principal**

Mentor

### **Objetivo**

Criar o perfil inicial do Mentor.

### **Pré-Condições**

-   O Mentor completou o Cadastro/Login no aplicativo.

### **Fluxo Principal**

1.  O Mentor acessa a área de cadastro de perfil.
2.  Preenche os campos obrigatórios:
    -   minibio\
    -   trilhas de especialidade\
    -   link da ferramenta de agendamento (ex.: Calendly)\
    -   foto\
3.  Clica em **Salvar** ou **Submeter**.

### **Campos Essenciais**

`nome`, `email`, `fotoUrl`, `minibio`, `trilhas`, `calendlyUrl`.

### **Pós-Condição**

Perfil é criado com status inicial **"Pendente"**.

------------------------------------------------------------------------

## **RF-MTR-02 -- Submeter Perfil para Aprovação**

### **Descrição**

Enviar o perfil para avaliação do Administrador.

### **Ator Principal**

Mentor

### **Objetivo**

Submeter o perfil para aprovação.

### **Pré-Condições**

-   O Mentor completou o cadastro do perfil (RF-MTR-01).

### **Fluxo Principal**

1.  O Mentor preenche todos os campos necessários do perfil.
2.  Submete o perfil.
3.  O sistema define o status do perfil como **"Pendente"**.
4.  O Administrador avalia e aprova o cadastro (Jornada Admin).
5.  O Mentor é notificado (RF-MTR-07).

### **Pós-Condição**

-   Se aprovado → perfil **Ativo** e elegível para matchmaking.\
-   Se reprovado → Mentor é notificado.

------------------------------------------------------------------------

## **RF-MTR-03 -- Registrar Mentoria**

### **Descrição**

Registrar uma mentoria agendada para ativar lembretes e acompanhamento.

### **Ator Principal**

Mentor

### **Objetivo**

Cadastrar uma mentoria já agendada externamente.

### **Pré-Condições**

-   Mentor recebeu um agendamento via ferramenta externa (ex.:
    Calendly).
-   Perfil do Mentor está **Ativo**.

### **Fluxo Principal**

1.  Acessa "Minhas Mentorias".
2.  Clica em **Registrar Nova Mentoria**.
3.  Informa mentorado, data e hora.
4.  Confirma o registro (`POST /mentorias/registrar`).

### **Pós-Condição**

Mentoria registrada com status **"agendada"** e lembretes ativados.

------------------------------------------------------------------------

## **RF-MTR-04 -- Marcar Presença e Preencher Feedback**

### **Descrição**

Finalizar o ciclo da mentoria preenchendo presença e feedback.

### **Ator Principal**

Mentor

### **Objetivo**

Informar presença e registrar feedback pós-mentoria.

### **Pré-Condições**

-   Data/hora da mentoria já ocorreu.

### **Fluxo Principal**

1.  Após a sessão, o Mentor acessa a mentoria.
2.  App libera o formulário de feedback.
3.  Mentor responde: *"O mentorado compareceu?"* (Sim/Não).
4.  Preenche campos adicionais opcionais.
5.  Submete (`POST /mentorias/finalizar`).

### **Pós-Condição**

-   Mentoria atualizada como **"concluída"** ou **"no-show"**.\
-   Se presença = Sim → libera avaliação para o mentorado.

------------------------------------------------------------------------

## **RF-MTR-05 -- Visualizar Histórico de Mentorias**

### **Descrição**

Mostrar todas as mentorias registradas pelo Mentor.

### **Ator Principal**

Mentor

### **Objetivo**

Acompanhar mentorias passadas e futuras.

### **Pré-Condições**

-   Mentor possui mentorias registradas.

### **Fluxo Principal**

1.  Acessa "Histórico" ou "Minhas Mentorias".
2.  Sistema lista todas as mentorias com status e detalhes.
3.  Mentor filtra por status (concluídas, agendadas etc.).

### **Pós-Condição**

Mentor visualiza seu histórico completo.

------------------------------------------------------------------------

## **RF-MTR-06 -- Editar Perfil**

### **Descrição**

Atualização dos dados do Mentor.

### **Ator Principal**

Mentor

### **Objetivo**

Permitir edição da minibio, trilhas, foto e link.

### **Pré-Condições**

-   Mentor já possui um perfil (RF-MTR-01).

### **Fluxo Principal**

1.  Acessa "Editar Perfil".
2.  Altera os dados desejados.
3.  Salva as alterações.

### **Pós-Condição**

Dados atualizados imediatamente no sistema e no matchmaking.

------------------------------------------------------------------------

## **RF-MTR-07 -- Receber Notificações**

### **Descrição**

Alertar o Mentor sobre eventos importantes.

### **Ator Principal**

Mentor

### **Objetivo**

Receber notificações push sobre perfis, agendamentos e avaliações.

### **Pré-Condições**

-   Estar logado e com push notifications ativadas.

### **Fluxo Principal**

1.  Notificação de aprovação do perfil.\
2.  Notificação de novo agendamento.\
3.  Notificação de avaliação recebida.

### **Tecnologia**

Firebase Cloud Messaging (FCM).

------------------------------------------------------------------------

## **RF-MTR-08 -- Ganhar Voucher por Mentoria Concluída**

### **Descrição**

Recompensar mentores ativos com vouchers.

### **Ator Principal**

Mentor

### **Objetivo**

Conceder um voucher por mentoria concluída com presença.

### **Pré-Condições**

-   Mentoria registrada (RF-MTR-03).
-   Presença marcada como **Sim** (RF-MTR-04).

### **Fluxo Principal**

1.  Mentor confirma presença no feedback.
2.  Sistema valida conclusão.
3.  Sistema ou Cloud Function gera e atribui voucher.
4.  Mentor recebe notificação.
5.  Voucher aparece em seu perfil de Mentorado.

### **Comentário**

Funcionalidade sugerida para **Fase 2** (não MVP).
