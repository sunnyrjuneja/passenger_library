---
title: Getting started with Meteor + Phusion Passenger
section: start
---
# Getting started with Meteor + Phusion Passenger

<p class="lead">This 5 minute tutorial teaches you to start your application in a Phusion Passenger server. Feel what Passenger is and how it works.</p>

## Install Passenger

Visit [the Passenger download page](https://www.phusionpassenger.com/download#open_source). There are tailor-made, polished installation methods for OS X, Debian/Ubuntu, Heroku, etc. :)

## Running the server

You normally run your app like this when in development mode, right?

~~~bash
meteor run
~~~

It's similar with Passenger. Instead of `meteor run`, you run your app with `passenger start`:

~~~bash
passenger start
# => ======= Phusion Passenger Standalone web server started =======
# => PID file: /Users/phusion/myapp/tmp/pids/passenger.3000.pid
# => Log file: /Users/phusion/myapp/log/passenger.3000.log
# => Environment: development
# => Accessible via: http://0.0.0.0:3000/
# => 
# => You can stop Phusion Passenger Standalone by pressing Ctrl-C.
# => ===============================================================
# => App 85125 stdout: [[[[[ ~/myapp ]]]]]
# => App 85125 stdout: 
# => App 85125 stdout: => Meteor server running on: http://localhost:9822/
~~~

We see a couple of things here:

 * Passenger reports that it has started a server, which is accessible via http://0.0.0.0:3000/. It also tells you where it has placed its PID file and log file.
 * Internally, Passenger runs your Meteor app by invoking the command `meteor run`. You can see the output of that command in the lines that are marked with "App xxx stdout". The xxx is the PID of the `meteor run` command.
 * `meteor run` starts its own server at http://localhost:9822/. But that's not the URL we want to access. Passenger listens on its own port, manages Meteor, and forwards requests to Meteor through the address http://localhost:9822/. So you should ignore this line.

So Passenger is now serving your app on [http://0.0.0.0:3000/](http://0.0.0.0:3000/). So if you go to that URL, you will should see your application:

~~~bash
curl http://0.0.0.0:3000/
# => your app's front page HTML
~~~

## Stopping the server

There are two ways to stop the server. The first is by pressing Ctrl-C in the terminal.

~~~bash
passenger start
# => ...
# => (press Ctrl-C here)
# => Stopping web server... done!
~~~

The second way is by starting a seperate terminal, changing the working directory to your application, and running `passenger stop`:

~~~bash
cd /path-to-your-app
passenger stop
~~~

## Conclusion

<p class="hidden-xs"><img src="../../images/award.png" alt="Achievement unlocked. Image taken from https://openclipart.org/detail/60109/award-symbol-by-sheikh_tuhin" class="pull-right"></p>
<p class="visible-xs text-center"><img src="../../images/award.png" alt="Achievement unlocked. Image taken from https://openclipart.org/detail/60109/award-symbol-by-sheikh_tuhin" width="128"></p>

Congratulations! Now that you've passed this tutorial and seen Passenger in action, you may be interested in intermediate-level walkthroughs.

Learn more about Passenger and its features:

<a href="../intro/meteor/" class="btn btn-primary">Read introduction walkthrough &raquo;</a>

Deploy your app to production:

<a href="../deploy/meteor/" class="btn btn-primary">Read deployment walkthrough &raquo;</a>

...or <a href="../..">go back to the front page</a>.