let url = 'https://newsapi.org/v2/top-headlines?country=ph&apiKey=82cac78296c1498eb3c962cf587c4b5c';

fetch(url)
    .then(response => {
        return response.json();
    })
    .then(data => {

        document.querySelector('body').setAttribute('class', 'bg-transparent');

        let container = document.createElement('div');
        container.setAttribute('class', 'container')

        let header = document.createElement('h2');
        header.setAttribute('class', 'text-center');
        header.innerText = "Top Stories in the Philippines";
        container.appendChild(header)
        document.querySelector('body').appendChild(container);

        let row = document.createElement('div');
        row.setAttribute('class', 'row');

        data.articles.forEach(news => {


            // Create a responsive container for each cards
            let cardContainer = document.createElement('div');
            cardContainer.setAttribute('class', 'col-lg-4 col-sm-6 col-xs-12 d-flex');

            // Attach it as a child of the row
            document.querySelector('body').appendChild(container);
            container.appendChild(row);
            row.appendChild(cardContainer);

            // Create the parent div with the card class
            let card = document.createElement('div');
            card.setAttribute('class', 'card border-light shadow p-3 mb-5 bg-white rounded');

            // Create the card-img-top child of the card
            let image = document.createElement('img');
            image.setAttribute('src', news.urlToImage);
            image.setAttribute('class', 'card-img-top');

            let hr = document.createElement('hr');

            // Create the card body to hold the title, description, and the link
            let cardBody = document.createElement('div');
            cardBody.setAttribute('class', 'card-body flex-fill');

            // Create the child card title of the card-body
            let cardTitleLink = document.createElement('a');
            cardTitleLink.setAttribute('href', news.url);
            cardTitleLink.setAttribute('target', '_blank');

            let cardTitle = document.createElement('h5');
            cardTitle.setAttribute('class', 'card-title text-justify');
            cardTitle.textContent = news.title;
            
            // Create the child card text of the card-body
            let cardText = document.createElement('div');
            cardText.setAttribute('class', 'card-text text-justify');
            cardText.textContent = news.description;

            let footer = document.createElement('div');
            footer.setAttribute('class', 'card-footer');
            
            // Create the child button of the card-body
            let read = document.createElement('a');
            read.setAttribute('class', 'btn btn-primary');
            read.setAttribute('href', news.url);
            read.setAttribute('target', '_blank');
            read.textContent = 'Read More';
            
            // Create the parent element of the source, and make it a link
            let sourceLink = document.createElement('a');
            sourceLink.setAttribute('href', 'https://www.' + news.source.name)
            sourceLink.setAttribute('target', '_blank');

            let source = document.createElement('p');
            source.setAttribute('class','source text-muted text-right');
            source.textContent = news.source.name;
            
            // Append the card to the responsive parent div
            cardContainer.appendChild(card);

            // Append the image child to the card div
            card.appendChild(image);

            cardTitleLink.appendChild(cardTitle);
            cardBody.appendChild(cardTitleLink);
            
            sourceLink.appendChild(source);
            cardBody.appendChild(sourceLink);

            cardBody.appendChild(hr);
            cardBody.appendChild(cardText);
            
            card.appendChild(cardBody);
            
            card.appendChild(footer);
            footer.appendChild(read);

        });

        let footer = document.createElement('footer');
        let footerText = document.createElement('p')

        footerText.setAttribute('class', 'footer text-center');
        footer.innerHTML = '<p>Made by Mark with <a href="https://newsapi.org/">News API</a></p>';

        footer.setAttribute('class', 'text-center');

        document.querySelector('body').appendChild(footer);
        footer.appendChild(footerText);

    })
    .catch(e => {
        console.log(`An error has occurred: ${e}`);
    });