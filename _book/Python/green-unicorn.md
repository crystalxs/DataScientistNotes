---
description: 'Reference: https://gunicorn.org/'
---

# Green unicorn

### Install

Before we use, don't forget to install it:

`pip install gunicorn` or `pip3 install gunicorn`

### Run your server

We don't want to use `app.run()` anymore in your `server.py` file.

You should now be able to run your server:

```text
$ gunicorn -D --threads 4 -b 0.0.0.0:5000 --access-logfile server.log --timeout 60 server:app parameters
```

Also note that using `-D` option on green unicorn makes it create a **daemon** process sitting in the background. If we want to test the server and see the error, omit `-D`.

### Kill process

To kill all of those processes you need to do a few steps:

```text
beast:master:~/courses/msds692-private/hw/recommender $ gunicorn -D --threads 1 -b 0.0.0.0:5000 --access-logfile server.log --timeout 60 server:app ~/data/glove.6B/glove.6B.50d.txt ~/github/msds692/data/bbc

beast:master:~/courses/msds692-private/hw/recommender $ ps aux | grep gunicorn
parrt            71972   0.0  0.0  4267768   1028 s003  S+   11:01AM   0:00.00 grep gunicorn
parrt            71743   0.0  1.1  4657032 354216   ??  S    11:01AM   0:06.19 /Users/parrt/anaconda3/bin/python /Users/parrt/anaconda3/bin/gunicorn -D --threads 1 -b 0.0.0.0:5000 --access-logfile server.log --timeout 60 server:app /Users/parrt/data/glove.6B/glove.6B.50d.txt /Users/parrt/github/msds692/data/bbc
parrt            71737   0.0  0.0  4310344  10396   ??  S    11:01AM   0:00.02 /Users/parrt/anaconda3/bin/python /Users/parrt/anaconda3/bin/gunicorn -D --threads 1 -b 0.0.0.0:5000 --access-logfile server.log --timeout 60 server:app /Users/parrt/data/glove.6B/glove.6B.50d.txt /Users/parrt/github/msds692/data/bbc

beast:master:~/courses/msds692-private/hw/recommender $ kill -9 71737

beast:master:~/courses/msds692-private/hw/recommender $ kill -9 71743

beast:master:~/courses/msds692-private/hw/recommender $ ps aux | grep gunicorn
parrt            72120   0.0  0.0  4267768   1028 s003  S+   11:02AM   0:00.00 grep gunicorn
```

As you can see, all of the processes for `gunicorn` are now dead. You kill the process ID to make them stop \(the number in the second column from `ps`\).

