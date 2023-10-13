# CArtAgO by exercises

The repository containing some exercises for learning the CArtAgO platform in depth.

## What is "CArtAgO"?

"CArtAgO" is a platform for programming environments in "Multi-Agent Systems", in order to elevate the "environment" as a first-class
abstraction. What this means is that not only you can program "agents" in MAS, as you can expect, but also the very thing they
use to communicate, coordinate and generally access the resources outside the system. CArtAgO follows the "Agents & Artifacts"
meta-model, which can be translated to "in an environment, everything is an artifact". An artifact is something that can be
acted upon by agents, through its operations making up their usage interface, and by other artifacts, through the operations
making up their linking interface. An artifact it can also be perceived, it can send signals and updates of its properties to
whoever agent decides to listen for them. Artifacts are collected in workspaces, which can in turn be collected in workspaces and
so on.

## What is "JaCaMo"?

We are not suggesting to use this platform on its own, au contraire, it exists a nice framework called "JaCaMo" which integrates
it with the agent programming language "Jason" and the organization specification language "MOISE". So, by using this framework,
and by cloning these repositories, you'll be able to program the artifacts but also the agents in order to solve the exercises.
How cool is that?

## What is "CArtAgO by examples" and how's different from what's here?

All the exercises in this repository have been heavily inspired by the "CArtAgO by examples" handbook. They have been slightly
changed in order to met the current Java code quality criteria, to exploit the newest features in the Java language to make the
life of developers easier, and to remove the unnecessary complexity not related to learning the "CArtAgO" platform.
We thought that transforming the examples into doable exercises, without having the solution right away,
will stimulate the learner to find a solution by themselves, possibly one which it is even better than the solution suggested.
For every exercise, a template for the files to create is given and their filling is left to the learner.
A solution is also given, but the explanation on why that solution is the right one can be found in the original manual.

## How to do the exercises?

You have to clone this repository with all its submodules using the command

```shell
git clone --recurse-submodules git@github.com:cake-lier/jacamo-by-exercises.git
```

Nothing else is required, all of them just work out of the box. So, enjoy playing with CArtAgO and JaCaMo!

## Useful resources

For first, obviously the original handbook from which the exercises were taken:

* [CArtAgO by examples](https://github.com/CArtAgO-lang/cartago/blob/b98b0e511a7e908a3fbaa54027e46f43f68cc406/docs/cartago_by_examples/cartago_by_examples.pdf)

The handbook explaining how does the "Jason" agent programming language works and its official documentation:

* [Jason's handbook](https://github.com/jason-lang/jason/blob/e6af9633060cdf5564263fc7bc3b94417ad6bf23/doc/Jason.pdf)
* [Jason documentation](https://www.emse.fr/~boissier/enseignement/maop13/doc/jason-api/jason/stdlib/package-summary.html)

The documentation referring on how does the format for JaCaMo configuration files works:

* [JaCaMo configuration file documentation](https://github.com/jacamo-lang/jacamo/blob/d7320760706cd67bcda7d5481aae5421a51a3dd0/doc/jcm.adoc)

Some notes on how the JaCaMo platform works, documenting a bit more some of what is available to developers:

* [Some help on the use of the JaCaMo platform](https://www.emse.fr/~boissier/enseignement/maop17-spring/doc/help.html)

As a conclusion, the competition, another list of exercises you can do about CArtAgO if you didn't had enough of ours:

* [A step by step walk in programming multi-agent environment](https://www.emse.fr/~boissier/enseignement/maop19-winter/env-step-by-step.html#_step_5_coordination_again_by_the_way_of_artifact)

## ⚠️⚠️⚠️ A word of advice before leaving you to the exercises ⚠️⚠️⚠️

Pay attention to the fact that the original "CArtAgO by examples" manual has not been updated since CArtAgO 2.0. Being now at
CArtAgO 3.0, some of the exercises could not be fully brought into this project. So, when checking for some explanation or for some
code examples, if it doesn't align with the solution we provide you or if it doesn't downright work, no worries! This is totally
to be expected and, you know, this is the reason for which this project has been brought to existence. This is also true for all
the other resources we linked in this repo.

If you want to see the changelog between CArtAgO 2.0 and 3.0, please refer to the corresponding [document](cartago3_changelog.md).

Another thing to note is that both "JaCaMo" and "CArtAgO" are work in progress, so bugs can be spotted. If you do, don't panic and
please report them to the [JaCaMo official repository](https://github.com/jacamo-lang/jacamo) and the [CArtAgO official repository](https://github.com/CArtAgO-lang/cartago).
