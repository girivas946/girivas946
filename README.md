const puppeteer = require('puppeteer');

(async function scrape() {
    const browser = await puppeteer.launch({ headless: false });

    const page = await browser.newPage();
    await page.goto('https://prefeitura.pbh.gov.br/saude/licitacao/pregao-eletronico-151-2020');

   // let data1;
   let i;
    let data = await page.evaluate(() => {
    	let data1='';
    	let y = document.body.querySelectorAll('.lbl-licitacao');
       // for (i = 0; i < y.length; i++) {
		    data1 += y[0].innerHTML+"\n\n";
		    data1 += y[1].innerHTML+"\n\n";
		    data1 += y[5].innerHTML+"\n\n";
		    // i+=2;
			  // }
        let x = document.body.querySelectorAll('a');
       for (i = 0; i < x.length; i++) {
		    data1 += x[i].href+"\n";
			  }

        return data1;

    });

    // logging results
    console.log(data);
    await browser.close();

})();
