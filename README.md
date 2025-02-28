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
