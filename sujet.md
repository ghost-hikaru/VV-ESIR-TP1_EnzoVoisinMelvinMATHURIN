# Practical Session #1: Introduction

1. Find in news sources a general public article reporting the discovery of a software bug. Describe the bug. If possible, say whether the bug is local or global and describe the failure that manifested its presence. Explain the repercussions of the bug for clients/consumers and the company or entity behind the faulty program. Speculate whether, in your opinion, testing the right scenario would have helped to discover the fault.

2. Apache Commons projects are known for the quality of their code and development practices. They use dedicated issue tracking systems to discuss and follow the evolution of bugs and new features. The following link https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-794?filter=doneissues points to the issues considered as solved for the Apache Commons Collections project. Among those issues find one that corresponds to a bug that has been solved. Classify the bug as local or global. Explain the bug and the solution. Did the contributors of the project add new tests to ensure that the bug is detected if it reappears in the future?

3. Netflix is famous, among other things we love, for the popularization of *Chaos Engineering*, a fault-tolerance verification technique. The company has implemented protocols to test their entire system in production by simulating faults such as a server shutdown. During these experiments they evaluate the system's capabilities of delivering content under different conditions. The technique was described in [a paper](https://arxiv.org/ftp/arxiv/papers/1702/1702.05843.pdf) published in 2016. Read the paper and briefly explain what are the concrete experiments they perform, what are the requirements for these experiments, what are the variables they observe and what are the main results they obtained. Is Netflix the only company performing these experiments? Speculate how these experiments could be carried in other organizations in terms of the kind of experiment that could be performed and the system variables to observe during the experiments.

4. [WebAssembly](https://webassembly.org/) has become the fourth official language supported by web browsers. The language was born from a joint effort of the major players in the Web. Its creators presented their design decisions and the formal specification in [a scientific paper](https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf) published in 2018. The goal of the language is to be a low level, safe and portable compilation target for the Web and other embedding environments. The authors say that it is the first industrial strength language designed with formal semantics from the start. This evidences the feasibility of constructive approaches in this area. Read the paper and explain what are the main advantages of having a formal specification for WebAssembly. In your opinion, does this mean that WebAssembly implementations should not be tested? 

5.  Shortly after the appearance of WebAssembly another paper proposed a mechanized specification of the language using Isabelle. The paper can be consulted here: https://www.cl.cam.ac.uk/~caw77/papers/mechanising-and-verifying-the-webassembly-specification.pdf. This mechanized specification complements the first formalization attempt from the paper. According to the author of this second paper, what are the main advantages of the mechanized specification? Did it help improving the original formal specification of the language? What other artifacts were derived from this mechanized specification? How did the author verify the specification? Does this new specification removes the need for testing?

## Answers
### Answer of question 1
The bug mentioned here is a known bug called the **the pentium bug**: the result of some float divisions was wrong. The error originates from the incomplete initialization of a table of values to use a redundancy of the numeration system used to represent the quotient.
It is therefore a local error, indeed the bug only occurred when certain specific divisions were made. Despite this, the processor worked very well.

The bug could have impacted the result of a researcher or other person looking for a very precise result at a division. For INTEL, the bug allowed the firm to change its way of doing things by publishing its algorithms and proofs online in order both to maintain user confidence and on the other hand to make errors more easily detectable by the audience.

([Ressources](https://interstices.info/les-lecons-dun-algorithme-delinquant/))
### Answer of question 2
After a search on the site, we are interested in issue #697 
([Bug in question](https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-697?filter=doneissues)).

In this one, someone explains that modifying an underlying list of a list of type FixedSizeList modifies the list of type FixedSizeList. There is no way to know if this is a local or global bug. Only several clues on the page can help us, indeed the problem was created in 2018 and solved in 2020. The fact that the bug was solved in 2 years can indicate that it was a local bug that did not have a big impact. However, the fact that the person indicated a **major priority** could indicate that it was a global bug that needed to be fixed quickly. The person proposes that the javadoc warns about this problem. Tests are then written so that the problem can be detected if it reappears in the future.

### Answer of question 3
_**Chaos Engineering**_ is the discipline of experimenting on a distributed system in order to build confidence in its capability to withstand turbulent conditions in production.

Netflix's priority is to deliver a service no matter what problems there may be. For them to keep their customers it is better to deliver a service (even if it has to be low quality) than to deliver nothing. This is understandable for the streaming domain in which Netflix is located. In order to implement this, Netflix has set up Chaos Engineering (using their **Chaos Monkey** software) which consists in killing servers randomly from a country and see if the users who were on this server continue to receive a service by moving them to another server. With the help of their software, they perform several tests to ensure that this problem works.

In order to perform these tests, Netflix needs:
* hypotheses,
* independent variables,
* dependent variables, 
* a context,

Netflix needs to observe:
- the steadystate behavior of the system, 
- SPS, for (stream) starts per second,

This allows them to see if their tests are working by looking at whether or not their customers are staying.
With all the tests performed Netflix was able to deduce the following results:
- 92% of catastrophic system failures were the result of incorrect handling of nonfatal errors,
- As time goes by, the number of tests and fault tolerance decreases and Netflix needs to automate the tests to ensure proper operation. Today Chaos Monkey runs continuously during the week when employees are in the office.

Netflix has been the precursor of this method of Chaos engineering. Today, several large companies use this method such as Amazon, Microsoft, Facebook or Google.

The goal of Chaos Engineering is to ensure that a service is always delivered in order to retain customers. To implement it, you need to make sure that the organization has several servers in order to redirect its customers. Or at least be able to simulate the fact of having several servers. Then the organization must agree on the variables to be analyzed, the hypotheses to be made and finally the context. 

### Answer of question 4
The main advantages of having a formal specification for WebAssembly is that the language is safer and faster to execute. It makes it possible to obtain a very strong assurance of the absence of bugs in the software. 
In my opinion, WebAssembly implementations should still be tested, because at the end, the programmer who will code a WebAssembly implementation is only human, and this human can make mistakes that will compromise the very strong assurance of the WebAssembly implementations. 

### Answer of question 5
The Mechanical Specification has some advantages: it is safer because the specification is examined by software, using mathematical proofs. By using this, it helps to highlight some issues found in the former version. The Mechanical Specification, as before with the formal specification, does not stop from using tests because an issue can be found in the software that examines the code.

As before, testing is necessary, but this time to check whether the software checking the problems is effective and does not encounter any problems. So we can add security by testing on the WebAssembly output. 

The artifacts derived from the mechanization are typechecker and executable interpreter. We verify the specification with the test, artifacts or interpreter for example.
