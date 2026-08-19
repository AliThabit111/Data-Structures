// Objective: Evaluate a Postfix (Reverse Polish) expression containing multi-digit numbers using a Stack.
// Logic: Push numbers onto the stack; when an operator is found, pop the top two operands, evaluate, and push the result back.
// Time Complexity: O(n) where n is the length of the expression string
// Space Complexity: O(n) for the stack and buffer

#include <iostream>
#include <stack>
#include <cstring>
#include <cstdlib>

using namespace std;

// Check if character is a valid arithmetic operator
bool isOperator(char ch)
{
	if (ch == '+' || ch == '-' || ch == '*' || ch == '/')
		return true;
	return false;
}

// Perform calculation based on the operator
int performOperation(int op1, int op2, char op)
{
	int ans = 0;
	switch (op) {
	case '+':
		ans = op2 + op1;
		break;
	case '-':
		ans = op2 - op1;
		break;
	case '*':
		ans = op2 * op1;
		break;
	case '/':
		ans = op2 / op1;
		break;
	}
	return ans;
}

int main()
{
	char exp[1000], buffer[15];
	int op1, op2, x;
	stack<int> s;

	cout << "Enter a Postfix Expression: (e.g. 4 5 * )\n";
	cin.getline(exp, 1000);

	int len = strlen(exp);
	int j = 0;

	for (int i = 0; i < len; i++) {
		// Collect digits for multi-digit operands
		if (exp[i] >= '0' && exp[i] <= '9') {
			buffer[j++] = exp[i];
		}
		// Convert buffer to integer on space delimiter and push to stack
		else if (exp[i] == ' ') {
			if (j > 0) {
				buffer[j] = '\0';
				x = atoi(buffer);
				s.push(x);
				j = 0;
			}
		}
		// If operator, pop two operands, evaluate and push result
		else if (isOperator(exp[i])) {
			op1 = s.top();
			s.pop();
			op2 = s.top();
			s.pop();
			s.push(performOperation(op1, op2, exp[i]));
		}
	}

	cout << "Answer = " << s.top() << endl;

	return 0;
}
