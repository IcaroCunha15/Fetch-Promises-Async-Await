# Fetch-Promises-Async-Await

1. XMLHttpRequest (XHR)
● Propósito: A maneira original de fazer requisições HTTP assíncronas em
JavaScript.
● API: Baseada em callbacks. Você define funções para serem executadas em
diferentes estágios do ciclo de vida da requisição (por exemplo,
onreadystatechange).
● Complexidade: Pode ser verboso e levar ao "inferno de callbacks" (callbacks
aninhados) para sequências complexas de operações assíncronas.
● Recursos:
○ Suporta navegadores mais antigos.
○ Fornece controle granular sobre o processo da requisição.
○ Pode lidar com uma ampla gama de protocolos além do HTTP.
● Integração com Promises: Não usa Promises inerentemente. Você precisa
envolvê-lo em uma Promise para trabalhar com padrões assíncronos mais
modernos.
2. API fetch
● Propósito: Uma maneira mais moderna e poderosa de fazer requisições HTTP
assíncronas.
● API: Baseada em Promises. A função fetch() retorna uma Promise que resolve
para o objeto Response (representando a resposta do servidor). Você então usa o
encadeamento .then() para lidar com a resposta e extrair os dados (o que
também retorna uma Promise).
● Complexidade: Geralmente mais limpo e legível do que XMLHttpRequest,
especialmente para cenários complexos devido à sua natureza baseada em
Promises.
● Recursos:
○ Fornece uma API mais intuitiva e flexível.
○ Suporta Promises nativamente.
○ Separa as preocupações de buscar o recurso e extrair os dados.
○ Oferece recursos como fluxos de requisição e resposta.
○ É o padrão para o desenvolvimento web moderno.
● Integração com Promises: Construído diretamente sobre Promises.
Claro, aqui está a tradução para o português da comparação entre XMLHttpRequest,
fetch, Promises e async/await em JavaScript:
Comparação entre XMLHttpRequest, Fetch, Promises e Async/Await em JavaScript
Vamos comparar XMLHttpRequest, fetch, Promises e async/await em JavaScript,
focando em seus papéis no tratamento de operações assíncronas, particularmente
requisições de rede.
1. XMLHttpRequest (XHR)
● Propósito: A maneira original de fazer requisições HTTP assíncronas em
JavaScript.
● API: Baseada em callbacks. Você define funções para serem executadas em
diferentes estágios do ciclo de vida da requisição (por exemplo,
onreadystatechange).
● Complexidade: Pode ser verboso e levar ao "inferno de callbacks" (callbacks
aninhados) para sequências complexas de operações assíncronas.
● Recursos:
○ Suporta navegadores mais antigos.
○ Fornece controle granular sobre o processo da requisição.
○ Pode lidar com uma ampla gama de protocolos além do HTTP.
● Integração com Promises: Não usa Promises inerentemente. Você precisa
envolvê-lo em uma Promise para trabalhar com padrões assíncronos mais
modernos.
Exemplo (Conceitual):
JavaScript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://api.example.com/data');
xhr.onload = function() {
if (xhr.status >= 200 && xhr.status < 300) {
// Sucesso
const data = xhr.responseText;
// ... processar dados
} else {
// Erro
console.error('Requisição falhou');
}
};
xhr.onerror = function() {
console.error('Houve um erro de rede.');
};
xhr.send();
●
2. API fetch
● Propósito: Uma maneira mais moderna e poderosa de fazer requisições HTTP
assíncronas.
● API: Baseada em Promises. A função fetch() retorna uma Promise que
resolve para o objeto Response (representando a resposta do servidor). Você
então usa o encadeamento .then() para lidar com a resposta e extrair os
dados (o que também retorna uma Promise).
● Complexidade: Geralmente mais limpo e legível do que XMLHttpRequest,
especialmente para cenários complexos devido à sua natureza baseada em
Promises.
● Recursos:
○ Fornece uma API mais intuitiva e flexível.
○ Suporta Promises nativamente.
○ Separa as preocupações de buscar o recurso e extrair os dados.
○ Oferece recursos como fluxos de requisição e resposta.
○ É o padrão para o desenvolvimento web moderno.
● Integração com Promises: Construído diretamente sobre Promises.
Exemplo:
JavaScript
fetch('https://api.example.com/data')
.then(response => {
if (!response.ok) {
throw new Error(`Erro HTTP! status: ${response.status}`);
}
return response.json(); // Ou response.text(), response.blob(), etc.
})
.then(data => {
// ... processar dados
console.log(data);
})
.catch(error => {
console.error('Erro de fetch:', error);
});
●
3. Promises
● Propósito: Um objeto representando a eventual conclusão (ou falha) de uma
operação assíncrona e seu valor resultante. Eles fornecem uma maneira
estruturada de lidar com código assíncrono, tornando-o mais gerenciável do
que callbacks.
● API: Usa .then() para lidar com o resultado bem-sucedido e .catch() para
lidar com erros. Você também pode usar .finally() para código que deve
ser executado independentemente do resultado da Promise. Promise.all(),
Promise.race(), etc., ajudam a gerenciar múltiplas Promises.
● Relação com XHR e Fetch: Tanto XMLHttpRequest (quando envolvido) quanto
fetch podem produzir Promises, permitindo que suas operações assíncronas
sejam gerenciadas usando a API Promise. fetch é inerentemente baseado em
Promise.
● Conceitos-chave:
○ Estados: Pendente, Cumprida (Resolvida), Rejeitada.
○ Encadeamento: Chamadas .then() podem ser encadeadas para lidar
com operações assíncronas sequenciais.
○ Tratamento de Erros: .catch() fornece uma maneira centralizada de
lidar com erros em uma cadeia de Promises.
4. async/await
● Propósito: Açúcar sintático sobre Promises, fazendo com que o código
assíncrono pareça e se comporte um pouco mais como código síncrono.
Simplifica a sintaxe para trabalhar com Promises.
● API:
○ Palavra-chave async: Colocada antes de uma declaração de função
para indicar que a função retornará uma Promise.
○ Palavra-chave await: Usada dentro de uma função async para pausar a
execução da função até que uma Promise estabilize (seja resolvida ou
rejeitada). A expressão await retorna o valor resolvido da Promise (se
ela for resolvida) ou lança o valor rejeitado (se ela for rejeitada).
● Relação com Promises: async/await é construído sobre Promises. Toda
função async retorna implicitamente uma Promise, e await é usado para
esperar sincronamente que uma Promise seja resolvida.
● Tratamento de Erros: Usa blocos padrão try...catch para lidar com erros
que ocorrem durante o await de uma Promise.
● Legibilidade: Geralmente torna o código assíncrono mais fácil de ler e
entender, especialmente para fluxos assíncronos complexos.
Em essência:
● XMLHttpRequest é a maneira mais antiga e verbosa de fazer requisições web.
● fetch é o substituto moderno, baseado em Promise, para XMLHttpRequest.
● Promises são um recurso fundamental do JavaScript para gerenciar os
resultados de operações assíncronas, usado por fetch e pode envolver
XMLHttpRequest.
● async/await fornece uma sintaxe mais semelhante à síncrona para trabalhar
com Promises, tornando o código assíncrono mais fácil de ler e escrever.
Para o desenvolvimento web moderno, fetch junto com async/await é a
abordagem preferida para lidar com requisições de rede assíncronas devido à sua
sintaxe mais limpa e natureza baseada em Promise.
