# Slash-Framework
Slash Framework
# slash command
slash command
python -m venv name_of_virtual_env
.\Scripts\activate
slash list .\test_exception.py
slash run -f asl.txt(asl file execution command)
slash run .\test_class.py -q(remove warning)
slash run .\test_exception.py -k tag:LowFuelLevelException(using tag )
slash list parametrizing_test --only tests
slash run .\test_class.py -k tag:sanity(tag)
slash run .\test_class.py -k tag:sanity -l log(collecting log)
slash run -vv .\test_class.py (This is test last log, this is cleanup)
slash run test_file.py -k requires --with-xunit --xunit -filename report.xml(detail report)


# slash basic information
Developing Test:
writing test,parameter,tag,logging error and exception,cleanup,skips,fixtures,test details

Writing test:
method based
class based method

@slash.parameter
declare before the test function

@slash.parameteriz("a",[1,2,3])


@tag are used to filter purpose

logging ,error and Exception:
Logging are handled by logbook packages by default slash prints the log in console.
to store the log in a file -l is used to redirect the log to path.
verbosity is handled by -v/-q
Log will be stored in {session_id}\debug.log
slash run .\test_class.py -k tag:sanity -l log
debug log
session log


Addition errors and Exception:
slash.add_error(msg) is used to add error to the current test result.
slash.add_failure(msg) is used to add failure to the current test result

cleanup:
slash provide a feature call cleanup which basically executes at the end of the test or module or session based on it's scope
to add cleanup use
slash.add_cleanup().Params
critical:if true ,execute even if the user interrupts the test
Sucess_only:If True excute this cleanup only if no error are encountered.
scope-Scope: at the end of which this cleanup will be executed.
args positional argument to pass to the cleanup function.
kwargs:keyword arg to pass to the cleanup function

skipped test case:
slash provide option to skip execution of test
skip test can be achieved using below ways:
class slash.exception.SkipTest(reason='Test skipped')
this exception should be raised in order to interrupt the execution of tge currently running test, marking it as skipped.

slash.skipped(thing,reason=None)
a decorator for skipping method and classes

slash.skip_test(*args)
skips the current test execution by raising a slash.exceptions.SkipTest exception.it can optionally receive a reason arguments

slash.register_skip_exception(exception_type)
registers a custome exception type ato be recognizes a test skip.this make the exception behave just as if the test called skip test

details:
slash support additional details about the test run by attaching the data to global or test result object.

to set detail for a session.add the detail to global result object
slash.context.session.results.global_result.set_test_detail("detail_name",value)
value can be string ,float,list or dict

to set detail for test result
slash.context.result.set_test_detail("detail name",value)

command:
slash run test_file.py -k requires --with-xunit --xunit -filename report.xml

hooks:
hooks are endpoint to which you can register callbacks to be called in specific points in a test session lifetime
To register a method to be executes in specific end point 
The method has to decorated as
@slash.hooks.hook_name.register

plugin:
slash provide development of plugins. Which are use for extending the behavior of slash
plugin should be used only for helping out in performing action around test and not performing any testing
1.built in plugin:
Xunit plugin which generate xunit xml report for the slash.
Coverage plugin tracks and reports runtime code coverage
Notification plugin allows user to be notified when session end or any notification end point to be generated
2.Create:Plugininterface(slash.plugins)
method:get_name and configure_arguments_parser , configure_from_parsed_args()
3.use
