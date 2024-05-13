  Este é um script Python que interage com o serviço de chatbot da Verbeux, utilzado na metodologia de fluxo, e um banco de dados no Firebase para coletar feedback dos usuários, a estrutura do código é separada em três principais tópicos:
  1. importações e bibliotecas:
     - requests: Uma biblioteca utilizada para fazer solicitações HTTP,
     - json: Uma biblioteca para o banco de dados que está armazenada em dados json.

  2. Variáveis:
     - snapshot_version: Versão snapshot do CHATBOT.
     - api_key: A chave API para acessar o serviço do CHATBOT.
     - link_firebase: O URL do banco de dados Firebase.
       
  3. Funções:
     - get_new_chat(): Envia uma solicitação POST para o serviço de chatbot para obter uma nova conversa. Retorna os dados da nova conversa.
     - send_message(chat_id, message): envia uma mensagem para o chat identificado por chat_id e retorna a resposta do chatbot.

  4. Lógica principal:
     - No bloco if __name__ == "__main__":, o script começa obtendo uma nova conversa através da função get_new_chat(). Em seguida, entra em um loop infinito onde o usuário é solicitado a fornecer mensagens,         que são enviadas para o chatbot e as respostas são impressas.

     - Dependendo da mensagem do usuário o CHATBOT terá ações diferentes, temos todas as funcionalidades a seguir:
        - Para iniciar uma conversa com o CHATBOT é preciso enviar uma mensagem de saudações. Exemplos: "Hello" ou "Hi".
        - Após a mensagem de saudação, você poderá enviar qualquer mensagem de feedback, tanto uma reclamação quanto um elogio, ele irá responder a mensagem de acordo com conteúdo dela, se ele não entender              apenas esclareça qual o tipo de feedback enviado com um "Positive" ou "Negative", de acordo com o tema escolhido. É possível enviar feedbacks infinitamente, todos os feedbacks enviados vão ser                 guardados em um banco de dados firebase.
        - É possível acessar o banco de dados com duas mensagens, para pegar todos os feedbacks positivos e os negativos, apenas envie as respostas "What are the positive feedbacks?" ou "What are the                    negative feedbacks?". Abaixo aparecerar a lista de todos os feedbacks registrados no banco de dados.
        - Para finalizar a conversa com o CHATBOT envie uma mensagem de despedida como um "Goodbye".
