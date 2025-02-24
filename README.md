# Explicação do Código

Este script automatiza o envio de mensagens via **WhatsApp Web** para contatos armazenados em um banco de dados **MySQL**. Ele também registra números já utilizados em uma planilha **Excel**, evitando mensagens duplicadas.  

## 📌 Bibliotecas Utilizadas

- `webbrowser`: Abre links no navegador.  
- `time`: Controla intervalos de espera entre as ações.  
- `urllib.parse`: Codifica a mensagem para ser enviada na URL.  
- `pyautogui`: Simula interações do teclado para enviar mensagens.  
- `pymysql.cursors`: Conecta ao banco de dados MySQL.  
- `openpyxl`: Manipula arquivos Excel.  

## 📂 Estrutura do Código

### 🔹 **Definição de Constantes**
O código define algumas variáveis importantes, incluindo a URL do **WhatsApp Web**, o arquivo de erro (`erros.csv`), o nome do arquivo Excel onde são armazenados os telefones enviados e as credenciais do banco de dados (mascaradas por `#####`).  

---

### 🔹 **Funções Principais**

#### 📌 `read_numbers_from_file(file_path)`
- Lê números de telefone de um arquivo **Excel** e os retorna como uma lista.  

#### 📌 `write_to_excel(file_path, phone_number)`
- Adiciona um número de telefone ao arquivo **Excel**, garantindo que não haja duplicação.  

#### 📌 `send_whatsapp_message(phone_number, message)`
- Monta um link do **WhatsApp Web** com o número e a mensagem formatada.  
- Abre o link no navegador, espera alguns segundos e simula o pressionamento de `Enter` para enviar a mensagem.  
- Fecha a aba após o envio.  

#### 📌 `log_error(name, phone_number)`
- Caso ocorra um erro ao enviar a mensagem, o nome e o telefone do contato são registrados em um arquivo **CSV**.  

---

### 🔹 **Fluxo Principal (`main()`)**
1. **Conecta ao banco de dados** MySQL usando `pymysql.connect()`.  
2. **Lê os números já enviados** do arquivo **Excel** para evitar duplicatas.  
3. **Busca novos contatos no banco de dados** que ainda não foram processados.  
4. **Para cada contato encontrado:**
   - Se o valor do pagamento (`pagamento_total`) for `"0"` ou `"300"`, o contato é ignorado.  
   - Caso contrário, gera-se uma mensagem personalizada.  
   - Se o número já estiver na lista de enviados, pula para o próximo contato.  
   - Caso contrário, a mensagem é enviada e o número é registrado no **Excel**.  
5. **O processo se repete a cada 20 segundos**.  

---

### 🔹 **Execução do Script**
Se o script for executado diretamente (`if __name__ == '__main__':`), ele chama a função `main()`, iniciando todo o fluxo de envio das mensagens.  

---

## 🛠 **Melhorias Possíveis**
✅ Usar um arquivo `.env` para armazenar as credenciais do banco de dados.  
✅ Tratar melhor erros para evitar falhas inesperadas.  
✅ Melhorar a eficiência ao lidar com grandes quantidades de contatos.  

---

Esse código é útil para **automação de envios no WhatsApp** e pode ser adaptado para diversos contextos, como **confirmação de pagamentos, lembretes ou notificações automáticas**. 🚀
