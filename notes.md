TDD duel
========

Before we get started, the contents below are not always so black and white. The intention to polarize on topics is to ensure that people hear the most extreme sides of the coin, and think of middle ground by themselves.

Dynamics
--------
* Each round, a topic is chosen
* Each oponent will be assigned to defend one side of the fence, in a polarized way
* Time dynamics is as follows:
	1. Facilitator introduces topic and randomly assigns sides and the person who starts (30 seconds)
	2. First side (oponent A) prepares a question/attack (1 minute)
	3. Oponent B replies (2 minutes)
	4. Oponent A replies back (2 minutes)
	5. Oponent B wraps up (1 minute)
	6. Total time per topis: 6.5 minutes
* The whole session is introduced in 1 minute, where dynamics are explained
* The session wraps up with audience questions. Now the oponents can reply truthfully to their opinions (9 minutes)
* Total running time: 1 + (6.5 * 3) + 9 = 29.5 minutes

Topics and thoughts on TDD
--------------------------

### TDD vs BDD

#### BDD advocate
Attacks:

1. TDD does not test the most important thing: if requirements are being met!
2. By leveraging BDD, you can report team progress based on agreed upon acceptance criteria -- beat this, TDD!
3. BDD can be used to regression test legacy systems, as long as they have clear expectations on input and output
4. In TDD, you can easily achieve high coverage and still see epic failures when all components are linked. By leveraging a functional, e2e approach, this risk is avoided

Rebuttals:

1. If you do not have architecture and practices for easy e2e testing, you are in trouble anyway
2. Multiple:
	a) If you cannot trace a story back to something that benefits the user, why implement it, then?
	b) Stories should be minimal anyway, as per good agile practices


#### TDD advocate

Attacks:

1. BDD encourages you to write complex, hard to maintain code
2. Feature/story breakdown can become awkward (n:n relationships, tech vs non-tech stories)
3. Most stories are born in the UI, a part of a system that constantly challenges automation (due to low ROI on many occasions). BDD fails at those cases

Rebuttals:

1. Multiple:
	a) By putting too much focus on e2e, the ability to quickly implement test cycles (as in 3' red-green-yellow) is challenged
	b) TDD leads to better software design. Nothing keeps you from BDD'ing a big ball of mud
2. 
3. TDD can be used on legacy systems as well, frequently in a more efficient manner than BDD. By skipping the obligation to tie tests to AC, you can automate the test of parts of complex, legacy features
4. You can still run integrated tests through BDD. All it foregoes is the need for a rigid tie back into ACs. 

### Mockist vs classicist

#### Mockist advocate

Attacks:

1. Full tests are not FAIR (or make it very hard to achieve): if your test does too much, there's a good chance it will not be Fast or Repeatable. And they are not Isolated, if you take the word literally.
2. Database-touching tests are a pain to write and maintain. Isolate it!
3. External systems may not be available. They should be mocked!
4. Setup/teardown become a lot simpler, making them a) faster and b) easier to run "in chunks" (as in "run just the tests that broke on the last execution")

Rebuttals:

1. If you are full of indirections, you are designing your dependencies wrong
2. See argument #1. If you have a plethora of expectations, you have too many dependencies and your code is doing too much. You should refactoring
3. This helps ensure the contract between modules is being properly followed. Isn't that important?
4. While it may impact refactoring, it does bring additional awareness about method usage. That way your refactoring becomes safer

#### Classicist advocate

Attacks:

1. Mocking may cause your code to become full of indirections, added solely for the purpose of mocking
2. Setting up a plethora of expectations in your tests easily makes them unmanageable
3. You end up testing all internal calls of your code -- but is that relevant on the grand scheme of things?
4. Also on testing all internal calls, this makes refactoring a lot harder

Rebuttals:

1. Multiple:
	a) You make your tests fast with proper architecture
	b) You make your tests repeatable by avoiding side effects. There are multiple techniques for that
	c) The word "Isolated" is open for interpretation. Do you mean to tell me a method will be able to run "isolatedly" in production. If not, why isolate it in test? Also, if your dependencies run too deep, it's time to consider refactoring...
2. If you do not have a proper test data strategy in place, you are in trouble anyway. As for performance, you can use a number of local DBs (eg: h2, or dockerized DBs) to emulate prod behavior
3. Multiple:
	a) Nobody said anything about hitting external systems during tests -- they are not your system, after all :)
	b) But do consider stubbing over mocking -- makes your testing a lot simpler
	c) Also, consider some level of deeply integrated testing, hitting real external endpoints. They are time-savers when checking full system connectivity

### TDD is dead, long live TDD!

#### TDD advocate

Attacks:

1. TDD is a time-tested manner of asserting code stability. To develop without it means to go back to the old, dark days of "let's hope it works"
2. Testing first guarantees that you are not subjecting your test logic to your SuT logic
3. Testing first means you are testing. Testing later frequently generates testing technical debt (as in "we should write tests for this code, but there's no time")
4. Testing first makes your commits safer
5. Testing first leads you to better design
6. This non-TDD thing is a monolithic/frameworkish plot. When you have code that does too much, you are tempted to drop this good practice

Rebuttals:

1. Being intrusive is not a problem when this leads to better design
2. This assumption has been proved true time and time again. There may be complex problems to test, and even cases where there is not enough ROI. But just generally dropping the approach is downright lazy thinking
3. By rejecting the test-first approach, you lose a lot of benefits (see arguments 2-5)
4. Multiple:
	a) testless code is even more expense to maintain
	b) there may be cases where this is true, but you would be surprised at the frequency in which this is a failed assumption. You have to first try, truly try, before you dismiss TDD as fruitless. 
	c) also, even if parts of a system (or even a full system) are not TDD'able, the notion of dropping the practice altogether is a logical fallacy (throwing the baby with the water)
5. Oh, boy. In summary, TDD is not a silver bullet. The arguments in this line are like saying "medicine is not that great, since people still die of illnesses"
	a) it will be even less so without TDD
	b) fallacy: lack of coverage does not speak against TDD. Actually, these cases are interesting cases for automation. Besides, TDD should be complemented with other forms of testing
	c) no TDD does not guarantee that either. And you can use ATDD to cover that ground
	d) still better than no TDD :)
	e) same way as any practice, when incorrectly put in place, may cause it

#### TDD RIP advocate

Attacks:

1. TDD is too intrusive to design
2. TDD works on this non-proved notion that a magic, TDD-able design will eventually emerge
3. No TDD does not mean not testing. It means rejecting the test-first approach
4. Tests are be too expensive to create and maintain
5. Automated tests are still no warranty of code quality. Test may exist and pass and still:
	a) code may not be maintainable
	b) code may have issues in hard-to-test areas such as perf, scalability, resillience, security, etc
	c) code may not implement what the user wants
	d) code may be failing to test relevant scenarios
	e) bad test code may generate a false sense of security in the team

Rebuttals:

1. Multiple:
	a) See #3
	b) But there's little to no hard evidence of the benefits stated in TDD argument #1, just annedoctal cases
2. Yeah, it means the opposite: you are subjecting your real, production, code, to your test logic. Doesn't that sound wrong?
3. You can also generate test technical debt with TDD. Developers can easily cheat (see this github repo: url to that test passer in github) and generate code that is as bad as (or worse than) no test as all
4. You can implement quick, safe cycles by implementing the tests after the code is done. It should take the same time, or less (after all, you did not spend time waiting for failed tests). If you are not doing automated tests at all, there are other processes (code analysis, peer reviews) that can check code quality. And these processes are required even with TDD in place
5. 

Reference material
------------------

* DHH, Fowler, Beck discussion on TDD:
* Mocks are not stubs:
* 