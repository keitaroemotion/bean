# bean

Elastic Beanstalk deployment partial automation helper. Utilizing **eb** and *aws elasticbeanstalk* commandline API, trying to help partial automation of elastic beanstalk deployment procedure.

## description

In browser-basic operation on environment variables in elastic beanstalk, deployer have to be careful about each process, which key-value pairs they change, can cause human error or be costly to safely update these. Especially, if that deployment procedure is going to be repeated task, when the procedure gonna be shorter, it might be happy for members.
Since aws provides command-line tools to support these deployment procedure, it implies if this is going to be wrapped appropriately in bash script, it can be automated (or at least semi-automated) so no need to flip-flop between browsers and the other tabs/apps, and once a script is proved to be successful, the all you need to do it to reuse this script.

## requisite

`eb` and `aws cli`

On Mac OSX 10.14.x, `eb` can be installed with 

```
$ ./scripts/setup
```

For aws-cli, look at: [https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html]
(The working one is aws cli version 1.16.292)

## usage

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






