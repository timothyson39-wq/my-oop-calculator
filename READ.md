stage 5 explanation
A requirement revealed missing behavior when invalid input like hello caused the calculator to crash. The new test checks that the program prints an error and does not add anything to history.

Coverage revealed an unexecuted path in the error-handling code, such as invalid removal handling. The test becomes meaningful by asserting that the correct error message appears and the existing history remains unchanged.