# Plataforma de Telégrafo Morse

## Arquivos
- `index.html` → página do aluno com telégrafo animado, som, cronômetro e envio.
- `avaliador.html` → página do avaliador que lê os envios salvos.
- `apps-script/Code.gs` → backend em Google Apps Script para salvar na planilha e listar os registros.

## Como funciona sem CORS
Esta solução evita o problema clássico de CORS de duas formas:

1. **Envio do aluno**: usa `form POST` para o Web App do Apps Script dentro de um `iframe` oculto, sem `fetch`.
2. **Leitura do avaliador**: usa **JSONP** com `callback`, carregando os dados via `<script src="...">`.

## Estrutura da planilha
A aba criada automaticamente será:

`MORSE_MESSAGES`

Colunas:
1. `created_at`
2. `student_name`
3. `target_name`
4. `morse_message`
5. `translated_message`
6. `elapsed_seconds`
7. `submitted_at`
8. `user_agent`

## Passo a passo do Google Apps Script
1. Crie uma planilha Google nova.
2. Abra **Extensões > Apps Script**.
3. Apague o código padrão e cole o conteúdo de `apps-script/Code.gs`.
4. Salve o projeto.
5. Vá em **Implantar > Nova implantação**.
6. Escolha **Aplicativo da web**.
7. Em execução como: **você mesmo**.
8. Quem tem acesso: **Qualquer pessoa com o link**.
9. Implante e copie a URL do Web App.

## Onde colar a URL
No `index.html`, substitua:
- `const GAS_POST_URL = 'COLE_AQUI_A_URL_DO_SEU_WEB_APP';`

No `avaliador.html`, substitua:
- `const GAS_GET_URL = 'COLE_AQUI_A_URL_DO_SEU_WEB_APP';`

Use a mesma URL nos dois arquivos.

## Fluxo para os alunos
- Seta esquerda = ponto.
- Seta direita = traço.
- Enter = separa letras.
- Espaço = separa palavras.
- Botão enviar = manda para a planilha.

## Observação didática importante
Na página do aluno, a tradução está pronta no código apenas para teste técnico. Ela começa oculta. Para uso real, mantenha essa área escondida.

## Melhorias que eu recomendo para a próxima versão
- adicionar campo de turma;
- adicionar ID único da tentativa;
- mostrar ranking de tempo no painel do avaliador;
- permitir filtro por aluno, turma e data;
- bloquear envio sem pelo menos 3 letras.
