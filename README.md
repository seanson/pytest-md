# pytest-md

Plugin for generating Markdown reports for [pytest] results 📝

[pytest]: https://github.com/pytest-dev/pytest

## Installation

**pytest-md** is available on [PyPI][PyPI] for Python versions 3.6 and newer
and can be installed into your enviroment from your terminal via [pip][pip]:

```text
$ pip install pytest-md
```

[PyPI]: https://pypi.org/
[pip]: https://pypi.org/project/pip/

## Usage

The following example code produces all of the different pytest test outcomes.

```python
import random
import pytest


def test_failed():
    assert "emoji" == "hello world"


@pytest.mark.xfail
def test_xfailed():
    assert random.random() == 1.0


@pytest.mark.xfail
def test_xpassed():
    assert 0.0 < random.random() < 1.0


@pytest.mark.skip(reason="don't run this test")
def test_skipped():
    assert "pytest-emoji" != ""


@pytest.mark.parametrize(
    "name, expected",
    [
        ("Sara", "Hello Sara!"),
        ("Mat", "Hello Mat!"),
        ("Annie", "Hello Annie!"),
    ],
)
def test_passed(name, expected):
    assert f"Hello {name}!" == expected


@pytest.fixture
def number():
    return 1234 / 0


def test_error(number):
    assert number == number
```

With **pytest-md** installed, you can now generate a Markdown test report as
follows:

```text
$ pytest --md report.md
```

```Markdown
# Test Report

*Report generated on 25-Feb-2019 at 17:18:29 by [pytest-md]*

[pytest-md]: https://github.com/hackebrot/pytest-md

## Summary

8 tests ran in 0.05 seconds

- 1 failed
- 3 passed
- 1 skipped
- 1 xfailed
- 1 xpassed
- 1 error

## Results

<table>
<thead><th>Result</th><th>Test</th><th>Duration</th></thead>
<tbody>
<tr><td>Failed</td><td>tests/test_generate_report.py :: test_generate_report[normal]</td><td>0.0</td></tr>
...
```

## pytest-emoji

**pytest-md** also integrates with [pytest-emoji], which allows us to include
emojis in the generated Markdown test report:

```text
$ pytest --emoji -v --md report.md
```

```Markdown
# Test Report

*Report generated on 25-Feb-2019 at 17:18:29 by [pytest-md]* 📝

[pytest-md]: https://github.com/hackebrot/pytest-md

## Summary

8 tests ran in 0.06 seconds ⏱

- 1 failed 😰
- 3 passed 😃
- 1 skipped 🙄
- 1 xfailed 😞
- 1 xpassed 😲
- 1 error 😡
```

[pytest-emoji]: https://github.com/hackebrot/pytest-emoji

## Credits

This project is inspired by the fantastic [pytest-html] plugin! 💻

[pytest-html]: https://github.com/pytest-dev/pytest-html

## Community

Please note that **pytest-md** is released with a [Contributor Code of
Conduct][code of conduct]. By participating in this project you agree to abide
by its terms.

[code of conduct]: https://github.com/hackebrot/pytest-md/blob/master/CODE_OF_CONDUCT.md

## License

Distributed under the terms of the MIT license, **pytest-md** is free and open
source software.
