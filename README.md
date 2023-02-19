# Issues

## CI - Issue in code analysis step 

For analysis phase was suggested to use npm check for critical dependencies. In my opinion this wasn't the best idea due to nondeterminism involved in this step.
Despite JavaScript is not my main language, I worked with that a lot and keeping dependencies clean and smooth is relatively hard process which requires 
very good knowledge of Node.js ecosystem and development project itself. There are many reasons behind this but let's mention at leas one for all.

JavaScript is simply dynamically interpreted language. That's why it is very limited in detection of compatibility issues with 3rd party libs in comparison 
to strongly typed compilable languages. Due to this in JavaScript world especially for package managers like npm, yarn and similar are given best practices
saying how to set dependencies in order to get them resolved correctly. Anyhow, this is entirely let on developers and that's why resolving deps is critical 
phase of each project and that's why JS world comes with lock files to at least ensure that deps are resolved the same in different developers machines over the
time.

There are of course many scanners and other mechanisms trying to find vulnerabilities in JS packages which are then gradually reported to developers to let them
react on this quickly. That's the whole sense here in this udapeople project, but there's no reliable command to fix this. If `npm audit fix` is used with 
`--force` flag it may cause to reconstruct dependency tree in a way which is not any more with application code any more. That's exactly what I'm observing here.
To fix fully dependency tree, update all problems you need either luck or developers who have deep technical insight into project and know what is used why and
how to react on given deps issues. Some of them may need upgrades with some code changes (after testing), some of them may require complete replacement and again
introducing significant code changes.

I'm obviously not the only one who stuck on this step. One relatively helpful mentors help was [described here](https://knowledge.udacity.com/questions/901582).
From my point of view this is wrong approach, because forcing audit fix in CI analysis step means it's not actually applied to the code. Secondly there's a problem
with fact, that udapeople project is relatively old and used dependencies are so out of date or obsolete that neither force flag helps.

### Hints for making analysis phase more reliable for Udacity students

The concept of static code analysis phase in CI pipeline is very important but I would recommend for JS projects some other step. It's better to use some linter
with described rules and leave in code some issue like wrongly formatted line of code. For example if statement without curly brackets or something similar. Other
alternative would be to measure code coverage and require certain level like 80%/60% for line/branch coverage. To let developers fail is possible to comment out
some unit test which after uncommenting would bring developers to the right coverage. Intro to unit test code coverage would be also interesting part of this course.

I must say that didn't have too much time to dive deeper in development specifics of this project to introduce anything like this. That's why leaving it here as
feedback with hints for improvement of the course.

