## Bringing the power of NodeJS to web form bruteforcing...

[![Code Climate](https://codeclimate.com/github/foxjerem/node-bruteforce/badges/gpa.svg)](https://codeclimate.com/github/foxjerem/node-bruteforce)

A number of great open source bruteforce tools exist. However they are not able to handle the nonce-based CSRF protection embedded into Rails and Django. This tool addresses this by first grabbing the CSRF token from the login page and then sending a login POST request. It comes pre-configured for Rails Devise and Django Admin interface and supports custom configuration for other variations. An option to set the maximum number of concurrent requests prevents overloading the target server.

Please use responsibly!

### Setup

```shell
  $ git clone git@github.com:foxjerem/node-bruteforce.git
  $ cd node-bruteforce
  $ chmod 755 run.js
  $ npm install -g
  $ node-bruteforce
```

### Usage

```shell

  Usage: node-bruteforce -u <username> -w <wordlist> -t <target> [options]

  NodeJS HTTP(S) Login Form Bruteforcer

  Options:

    -h, --help               output usage information
    -V, --version            output the version number
    -u, --username <string>  login username
    -w, --wordlist <file>    dictionary file
    -t, --target <url>       target sign in url
    -N, --num-requests [n]   maximum concurrent requests (default 25)
    -T, --type [framework]   specify target framework
    -c, --config [file]      custom .json config file

  Examples:

    $ ./run.js -u root -w words.txt -N 50-t http://localhost:8000/admin -T django
    $ ./run.js -u admin@rails.com -w words.txt -N 35 -t http://localhost:3000/users/sign_in -T rails
    $ ./run.js -u root -w words.txt-t http://dvwa/login -c config/dvwa.json

```

### Custom Configuration

Rails Devise and Django Admin default login screens are supported by default through the -T flag. In case some settings have been modified or for applications with a similar set up, users can create a custom config file to use through the -c flag. See the [template](https://github.com/foxjerem/node-bruteforce/blob/master/config/custom/template.json) for a skeleton config to get started.

### Wordlists

A number of dependable wordlists can be found here:

+ [Linkedin 2012](http://www.adeptus-mechanicus.com/codex/hashpass/hashpass.php)
+ [RockYou](https://wiki.skullsecurity.org/Passwords)

### Test Suite

Test runs are handled via grunt. A mini web application instance is spawned at the beginning of the test suite to handle the http requests generated by the attack.

```shell

  $ grunt

  Running "env:dev" (env) task

  Running "run:mockServer" (run) task
  >> mockServer started
  [+] Starting mini web application on port 9000

  Running "jshint:files" (jshint) task
  >> 12 files lint free.

  Running "mochaTest:test" (mochaTest) task

```

