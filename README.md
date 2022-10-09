# Welcome to the you (auto)complete me Readme :computer: :memo:

**Author: Brendan Tuckerman**

[Github]()

**Stack & Libraries**

Built with 

- React [link]
- TailwindCSS [link]
- mL5.js CharRNN [Link] 
- Lexicon [Link]


**Poets & Works**

Emily Dickinson [link]
Model derived from: https://www.gutenberg.org/cache/epub/12242/pg12242.txt

William Shakespeare [link]
Complete Works model derived from: https://www.gutenberg.org/cache/epub/100/pg100.txt

Sonnets model derived from:  https://www.gutenberg.org/cache/epub/1041/pg1041.txt

Edgar Allan Poe [link]


**Experimental Models**

TS Eliot [link]
Model derived from 'The Wasteland' and 'Prufrock and other Observations': https://www.gutenberg.org/ebooks/author/599

Robert Frost [link]
Model derived from: https://www.gutenberg.org/files/59824/59824-0.txt

**Overview:** 


This project is an example of a machine learning regression models in action. It uses the ML5  CharRNN library to suggest poetry in the style of Emily Dickinson, T S Eliot, Robert Frost and William Shakespeare.

    This is my letter to the world,
       That never wrote to me, --
    The simple news that Nature told,
       With tender majesty.

    Her message is committed
       To hands I cannot see;
    For love of her, sweet countrymen,
       Judge tenderly of me!



**Sample Works**

//TODO: Screenshots

1. Emily Dickinson

```

The winds of spring
— Would not straight the Clover — And how not and my Floods — And we and the 
lost sought a new path where
He could I do not see — The Sun — makes — and the say — The Summer heat
It was not a firm — But when the Firmament — When the Heaven — and the Bee —
only then
The Wind abode — more there — And not for the Hills — The Summer — say — only once--
The Grave an Art of the sun To still the room.


```

Edgar Allen Poe

```
   Where do they lie?
   to be destruction of the contrary, which has
   Never seen this
   I cannot read!--the bowers of the breath and forever
   litter a star which the beautiful bed light
   lines. But the most spirit from the first thought
   Cannot reach me.

```

**Some other notable lines:**

"Ha! ha! ha! ha! ha! ha! ha! ha! ha! ha! ha! ha!" - Edgar Allan Poe

##  About / Tutorial: Training a model using CharRNN

- [x] Develop an environment.

    Training a model with the CharRNN library requires access to tensorflow, which in turn requires some pretty simple Python scripting. The instructions for how to do this can also be found in the [github for the CharRNN library](). 
    
    Be sure to use Python 3.6 as per the instructions. 

    To prepare the environnment:

    Check which versions of Python you have using 

    `$ python --version`

    You might need to download Python 3.6 for your OS.

       
   Also ensure that you have installed `pip`, which is the package manager for Python.

   We are going to use `pip` and `python 3.6` to set up a virtual environment on our machine, so that it does not interfere with any local Python on our machine.

   I used [virtualenv](https://virtualenv.pypa.io/en/latest/) to set up my Python virtual environment, but `venv` should also work.

   To install virtualenv open the console and use

   `pip install virtualenv`

   Once we have virtualenv, we can create an environment using 

   `virtualenv -p python3.6 YOUR_ENV_NAME_HERE`

   It doesn't really matter where you create your environment, but you might like to keep it seperate from any final projects (like a front-end to dispaly the output), as you will be cloning a repo into this environment. You can copy the models produced in this environment easily. 

   The environment is now created. 

   We have to activate this new environment with

    `source YOUR_ENV_NAME_HERE/bin/activate`
    
   You should now see that your terminal is in a new Python sub terminal, and your machine is ready to learn.
     

- [x] Train the model using the text files.

   I used [this](https://www.gutenberg.org/ebooks/12242) version of Emily Dickinson's complete poems and created a new txt file, with everything but the poems removed.

   To do this, you can use a script like this: 

   (or just use the Regex search function inside VSCode)

   Check the size of your file--you want as much data as possible (but your training might take a while).

   The next set of instructions are as per the github instructions for training a model. 

   ```bash

   $ git clone https://github.com/ml5js/training-charRNN
   $ cd training-charRNN
   $ pip install -r requirements.txt
   $ python train.py --data_path /path/to/data/file.txt

   ```

   Depending on the size of your text file, you might like to set some [hyperparameters](https://github.com/ml5js/training-charRNN#hyperparameters). The size of your file will also impact the speed of the training -- my Dickinson and Eliot training took about a minute, while the original Shakespeare full text I tried using was scheduled to run for 14 hours.

   TODO: You can set the hyperparameters as flags...

   Once the training is complete, you can find the models you made in the `models/` folder. You'll need to copy the entire thing into your project so you can access them.

         

- [x] Generate predictions using the model
   
   NB: Using the ml5 library from localhost results in CORS errors. You might notice that if ou try to create a basic HTML template and then try to run your page, you will get a 404 error in the console.

   To avoid this, one solution is to run this project as a live server. I used **Live Server**, which is available as an extension with VS Code.

   In React placing the models into the `public` folder helped to overcome the same issues.

   To see your model in action, you can create a basic HTML file using this boiler plate from ml5:
      
      ```html
         <!DOCTYPE html>
         <html lang="en">
         <head>
            <title>Getting Started with ml5.js</title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>
         </head>

         <body>
            <script>
               // Your code will go here
               // open up your console - if everything loaded properly you should see the correct version number
               console.log('ml5 version:', ml5.version);
            </script>
         </body>
         </html>
      ```
      
   The instructions on the [ml5](https://learn.ml5js.org/#/reference/charrnn) site are excellent and clear, and I'm simply reproducing them here.

   Once you have the basic HTML in place, you can add the following to the `<script>` tags:

   ```javascript

      // Create the character level generator with a pre trained model
      const rnn = ml5.charRNN('models/bolaño/', modelLoaded);

      // When the model is loaded
      function modelLoaded() {
         console.log('Model Loaded!');
      }

      // Generate content
      rnn.generate({ seed: 'the meaning of pizza is' }, (err, results) => {
         console.log(results);
      });

   ```

   Just be sure that you correctly point  `charRNN()` to the path where you have the models.

   [TODO: Variables in rnn.generate]

   And that is it! If you open the console, you should firstly see that the Ml5 library is connected. Then you will return an object with a key `sample`, which is has been generated from your model!


- [] Create a front end to allow users to enter text,  and then have the model supply the next line

   There are many rich text editors available, but this project makes use of Lexical, which has been recently released as open-source by Meta.



## Wishlist / Future Additions

- [] Translate the project to Typescript

- [] Further models, refining the current models

## Known Bugs / TODO :bug:

- [] Default seed needs to be set, to prevent gibberish being produced.

## Inspiration 

[Selected Stories](https://cvalenzuela.github.io/Selected_Stories/)

[Nabil Hassein's generative DOOM](https://nabilhassein.github.io/generative-DOOM/)


## Resources and tutorials:

[Python virtualenv on ArchLinux](https://wiki.archlinux.org/title/Python/Virtual_environment)

[ML5.js Library](https://learn.ml5js.org/#/)

[Project Gutenberg](https://www.gutenberg.org/)

[Working with Lexical](https://github.com/facebook/lexical)

[CharNNN Library from ML5](https://learn.ml5js.org/#/reference/charrnn)

[Creating a VirtualEnv to run the Python needed to train a model](https://www.youtube.com/watch?v=nnhjvHYRsmM)

[Training a CharNNN using the model in ml5.js](https://github.com/ml5js/training-charRNN)

[Text Generation with LTSM and Spell](https://www.youtube.com/watch?v=xfuVcfwtEyw)