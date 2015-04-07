# [fit] Ungemifying your projects

### (one repo to rule them all)

---

let's talk about

# [fit] MONORAILS

---

# What's a monorail?

A rails app that does *everything*

1. The Website
2. Background Jobs
3. Search
4. 3rd party service interaction
5. Kitchen sink duties

![right, 150%](simpsons-mono-rail.jpg)

---

# Why are monorails bad?

* No clear separation of concerns
* All code is loaded, even if you don't use it
* Scaling concerns (naïve scaling means everything is scaled)
* Test suite runs everything by default

---

# What can we do?

Let's split up app into separate pieces!

Models are usually the only thing needed in each component, so let's just gemify that.

---

# The code

```ruby
# Gemfile
gem 'mycompany-models',
    git: 'git@github.com:mycompany/mycompany-models.git',
    branch: 'master'
```

```
# Gemfile.lock
GIT
  remote: git@github.com:mycompany/mycompany-models.git
  revision: 976fea8d33e36ce3d63b08375626b6475b1f8ac2
  branch: master
  specs:
    mycompany_models (1.6.11)
      activerecord (~> 3.2.6)
      activesupport (~> 3.2.6)
```

--- 

# Workflow

1. Push code to master branch of `mycompany-models`
2. Update downstream projects:

```sh
# in terminal
bundle update mycompany-models
```

---

# Downsides of gemifying

* Code changes between gemified project and downstream project are tied together
* Multiple pull requests for the same issue!




