# <h1 align="center"> Puppeteer  <h1>
  ## <h2 align="center"> Desafio Robô Correios  <h2>

<hr/>
  
  <p>O desafio tem como proposta fazer o robô executar os seguintes passos abaixo: </p>
  
  1. Abrir o Chrome,
  2. Navegadar até o site do correios.com.br,
  3. Digitar um CEP no input de "Busca CEP",
  4. Apertar o Enter ou clicar na lupinha,
  5. Extrair os dados da página de resultado e exibir no terminal.
 <hr/>
  
  ### <h3>Abaixo o código o desafio proposto:</h3>
  
~~~shell
  
  const puppeteer = require('puppeteer');

    (async () => {
      //1. Abrir o Chrome
      const browser = await puppeteer.launch({headless: false});
      const page = await browser.newPage();
  
      //2. Navegadar até o site do correios.com.br,
      await page.goto('https://www.correios.com.br/');
      await page.waitForNetworkIdle();

      //Usei o evalaute para poder fazer alterações na pagina
      await page.evaluate(() => {
        //Abaixo removo o atributo target do form para não redirecionar para uma outra aba
        document.querySelector('#relaxation').closest('form').removeAttribute('target');
      });
  
      //3. Digitar um CEP no input de Busca CEP
      await page.type('#relaxation', '06455000');
  
      //4. Apertar o Enter ou clicar na lupinha
      await page.keyboard.press('Enter');
  
      //5. Extrair os dados da página de resultado e exibir no terminal.
      await page.waitForSelector('table#resultado-DNEC td');
      const conteudo = await page.evaluateHandle(() => document.querySelector('table#resultado-DNEC').innerHTML);
      console.log(conteudo);

      await browser.close();
 
})();
  
~~~
