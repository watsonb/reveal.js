# Presenting This Training Material

Greeting Dinohead trainer.  The training material you will be presenting is
contained in this Git repository.  If you're reading this document locally,
you've likely arleady cloned the repo, so good job.

There are, of course, a couple of other things to do to make this "presentation
worthy".

## Getting Your Environment Ready to Present

We'll be using the [reveal.js](https://revealjs.com/) framework to actually
present the slides on the screen.  This particular training was developed in
such a way that you run a small webserver pointed to the root of this repo,
then in a browser, navigate to localhost/<presetation_to_give>.html and you're
off and running.

And therein, lies the rub.  What webserver?  Any will do really, but this thing
is already backed by NodeJS NPM packages and ready to fly with that, so let's
just use it.

### Get NodeJS

I don't care how you do it, distro package provider, download installer from
[nodejs.org](https://nodejs.org/en/download/), use [nvm](https://github.com/nvm-sh/nvm),
etc; but you need to get NodeJS installed on your system.

You'll need 10.0.0 or later.  I've tested with Node LTS Dubnium (v10.12.1) and
Node LTS Gallium (v16.13.1).

### Install Packages and Start Web Server

Go to the root of **this** repository and use npm to install packages and start
the webserver.

```bash
cd <path_to_repo>
npm install
npm start
```

### Navigate to your Training

Now pop open a web browser and navigate to:

http://localhost:8000/<your_training>.html
