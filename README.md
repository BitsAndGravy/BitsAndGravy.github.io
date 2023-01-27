<!DOCTYPE HTML>
<html>
    <head>
        <title>Freedom FHW</title>
        <meta charset="utf-8">
        <style>
            body {
                background-color: rgb(214, 249, 255);
                font-family: sans-serif;
            }
            
            h1 {
                color: rgb(0, 0, 0);
                font-family: Georgia;
            }
            
            h2 {
                color: rgb(22, 59, 87);
            }
            
            h3 {
                color: rgb(28, 68, 97);
                background-color: rgb(166, 227, 255);
            }
            
            h4 {
                color: rgb(54, 104, 138);
            }
            
            h5 {
                color: rgb(78, 140, 181);
            }
            
            #title-div {
                background-color: rgb(250, 202, 8);
                margin: 5px;
                padding: 30px;
                
            }
            
            #main-content {
                background-color: rgb(255, 87, 210);
                margin: 5px;
                padding: 10px;
                width: 60%;
                float:left;
            }
            
            #contact-info {
                background-color: rgb(13, 250, 21);
                margin: 5px;
                padding: 10px;
                float:right;
                width: 25%;
            }
        </style>
    </head>
    <body>
    /* 
My bookshelf!
See a few books I have read.

Press the "Restart" button to change the color of the books.

Sorry all of the text is so small...
I had a vision of books with the spines 
facing out on some shelves, and the face
outward on the other shelves... by the time
I got to the book information I had little space left.
*/

background(178, 227, 157);

//Bookcase
var bookCase = {
    width: 360, //Changes how wide the whole case is (from the middle)
    height: 288, //Changes how tall the case is (from the bottom)
    sideWidth: 18, //Changes width of the rects on the far left/right 
    shelf: {
        spacing: 87, //How much space is between each shelf
        height: 12, //How thick each shelf is
    }
};
    
    //Backing of the book shelf
    fill(77, 48, 21);
    rect(200 - bookCase.width / 2, 399 - bookCase.height, bookCase.width, bookCase.height);
    
    //Left side of case
    fill(189, 78, 23);
    rect(200 - bookCase.width / 2, 399 - bookCase.height, bookCase.sideWidth, bookCase.height);
    
    //Right side of case
    rect(200 + bookCase.width / 2 - bookCase.sideWidth, 399 - bookCase.height, bookCase.sideWidth, bookCase.height);
    
    //Shelves
    for(var i = 0; i < 7; i++) {
        rect(200 - bookCase.width / 2 + bookCase.sideWidth, 399 - bookCase.height + i * bookCase.shelf.spacing, bookCase.width - bookCase.sideWidth * 2, bookCase.shelf.height);
    }
    
//books with spine showing
    //Defining variables
    var book = {
        height: 15, //inverse of height; higher numbers make shorter books
        width: 15,
        //Do not know the best way to have JS choose a random color
        colorR: 225,
        colorG: 225,
        colorB: 225,
        xPos: 10,
        yPos: 10,
        num: 0,
        spacing: 5,
        information: [
            {title: "The \nHobbit", author: "J.R.R\nTolkein", rating: "5/5"},
            {title: "Educated", author: "Tara \nWestover", rating: "5/5"},
            {title: "Eragon", author: "Chris\nPaolini", rating: "4/5"},
            {title: "1984", author: "George\nOrwell", rating: "4/5"},
            {title: "The Great\nGatsby", author: "F. Scott\nFitzgerald", rating: "3/5"},
            {title: "Animal\nFarm", author: "George\nOrwell", rating: "4/5"},
            {title: "Odyssey", author: "Homer", rating: "5/5"},
            {title: "Iliad", author: "Homer", rating: "3/5"},
            {title: "Maze\nRunner", author: "James\nDashner", rating: "3/5"},
            {title: "Kidnapped", author: "Robert\nStevenson", rating: "2/5"}
            ]
        };
    var i = 0; // i represents what shelf the books are on (this and next loops)
    var j = 0; // j represents which item from an array we are using (next loop)
    textSize(10); //Used in next loop
    
    //Loop for making the books - select random color/size
    while(i < 4) {
        book.xPos = 0;
        i++;
        while(book.xPos < bookCase.width - bookCase.sideWidth * 2 - 15) {
            book.height = random(15, bookCase.shelf.spacing - bookCase.shelf.height - 35);
            book.width = random(10, 25);
            book.colorR = random(-134, 479);
            book.colorG = random(-140, 429);
            book.colorB = random(-130, 563);
            fill(book.colorR, book.colorG, book.colorB);
        //Draw the books
        //book.yPos is where the first shelf rests
        book.yPos = 225 - bookCase.height + book.height; 
        rect(book.xPos + 200 - bookCase.width / 2 + bookCase.sideWidth, book.yPos + i * bookCase.shelf.spacing * 2, book.width, bookCase.shelf.spacing -  book.height);
        //Make sure that the books are right next to each other
        book.xPos += book.width;
        }
}

//books with face showing
    //Defining variables
    book.height = 72;
    book.width = 62;
    var i = 0;
    
    //Loop for making the books and applying title, author, and rating: - 
    while(i < 2) {
        i++;
        book.num = 0;
        while(book.num < 5) {
            book.colorR = random(-147, 452);
            book.colorG = random(-146, 488);
            book.colorB = random(-139, 465);
            fill(book.colorR, book.colorG, book.colorB);
            
            //Draw the books
            book.yPos = 225 - bookCase.height - book.height; 
            rect(47 + book.width * book.num, book.yPos + i * bookCase.shelf.spacing * 2, book.width - book.spacing, book.height);
            
            //Choose white text for dark books and vice versa
            if(book.colorR + book.colorG + book.colorB < 300) {
                fill(255, 255, 255);
            } else {
            fill(0, 0, 0);
            }
            
            //Book information
            text(book.information[j].title, 50 + book.width * book.num, 13 + book.yPos + i * bookCase.shelf.spacing * 2);
            text("by " + book.information[j].author, 50 + book.width * book.num, 39 + book.yPos + i * bookCase.shelf.spacing * 2);
            text("Rating: " +book.information[j].rating, 50 + book.width * book.num, 66 + book.yPos + i * bookCase.shelf.spacing * 2);
            //Make sure that the books are right next to each other
            book.num++;
            j++;
            }
}
    </body>
</html>
