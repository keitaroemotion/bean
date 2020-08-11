# bean

Elastic Beanstalk deployment partial automation helper. Utilizing **eb** and *aws elasticbeanstalk* commandline API, trying to help partial automation of elastic beanstalk deployment procedure.

## description

In browser-basic operation on environment variables in elastic beanstalk, deployer have to be careful about each process, which key-value pairs they change, can cause human error or be costly to safely update these. Especially, if that deployment procedure is going to be repeated task, when the procedure gonna be shorter, it might be happy for members.
Since aws provides command-line tools to support these deployment procedure, it implies if this is going to be wrapped appropriately in bash script, it can be automated (or at least semi-automated) so no need to flip-flop between browsers and the other tabs/apps, and once a script is proved to be successful, the all you need to do it to reuse this script.

## pre-requisites

`eb` and `aws cli`

On Mac OSX 10.14.x, `eb` can be installed with 

```
$ ./scripts/setup
```

For aws-cli, look at: [https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html]
(The working one is aws cli version 1.16.292)

## usage

firstly, open the ./scripts/bean and edit L1:

```
aws configure set default.region us-west-2
```

by default it sets its default region as us-wes-t2 so you need to fix it to fit the specific region you wanna deploy. (TODO: let user set this region externally)


after locating the `bean` script into /usr/local/bin with:

```
$ ./scripts/install
```

then first, you want to check which `ApplicationName` and `Environtname` you are going to update values.

```
$ bean list 
```

next, pick these `ApplicationName` and `Environtname` and set it as:

```
$ bean show [my-app-name] [my-env-name]
```

for enlisting the key value pairs of that environment variables.

finally, type something like:

```
$ bean update key1=value1 key2=value2 key3=value3 ...
```

Then you can deploy environment variables automatically.


## example

okay, here, you want to do something like:

- 1. set elb env variables `maintenance` to yes (to show maintenance pages)
- 2. in Heroku or something, deploy your app after pipe passed
- 3. set elb env variables `new-key1=new-value`, `key2=some-new-value`
- 4. set elb env variables `maintenance` to no (to stop showing maintenance pages)

then you need to make script something like:

```
#!/usr/bin/env bash

appname=my-app
envname=my-env

set -e
bean update $appname $envname maintenance=yes
heroku-cli deploy-the-latest-master-branch ## this is just an exmaple
bean update $appname $envname new-key1=new-value key2=some-new-value
bean update $appname $envname maintenance=no
```

DONE!!!! it looks much faster than opening aws console or you can easily test this script on staging server then after confirmed that it works fine, change the appname, envname or alpha....

so much more automated, IMAO.
