// Objective: Convert an Infix expression (e.g., A+B*C) to Postfix notation (e.g., ABC*+) using Stack.
// Operations: Operator precedence checking, Associativity handling, Parentheses management.
// Time Complexity: O(n)
// Space Complexity: O(n)

#include <iostream>
#include <stack>
#include <string>

using namespace std;

// Function prototypes
string InfixToPostfix(string expression);
int HasHigherPrecedence(char operator1, char operator2);
bool IsOperator(char C);
bool IsOperand(char C);

int main()
{
	string expression;
	cout << "Enter Infix Expression: \n";
	getline(cin, expression);
	string postfix = InfixToPostfix(expression);
	cout << "Output = " << postfix << "\n";
	return 0;
}

// Convert Infix expression to Postfix
string InfixToPostfix(string expression)
{
	stack<char> S;
	string postfix = "";

	for (unsigned int i = 0; i < expression.length(); i++) {
		// Ignore spaces or commas
		if (expression[i] == ' ' || expression[i] == ',') continue;

		// If character is an operator (+, -, *, /, $)
		else if (IsOperator(expression[i]))
		{
			while (!S.empty() && S.top() != '(' && HasHigherPrecedence(S.top(), expression[i]))
			{
				postfix += S.top();
				S.pop();
			}
			S.push(expression[i]);
		}
		// If character is an operand (letter or digit)
		else if (IsOperand(expression[i]))
		{
			postfix += expression[i];
		}
		// If opening bracket
		else if (expression[i] == '(')
		{
			S.push(expression[i]);
		}
		// If closing bracket, pop until matching '('
		else if (expression[i] == ')')
		{
			while (!S.empty() && S.top() != '(') {
				postfix += S.top();
				S.pop();
			}
			S.pop();
		}
	}

	// Pop remaining operators
	while (!S.empty()) {
		postfix += S.top();
		S.pop();
	}

	return postfix;
}

// Check if character is operand (letter or number)
bool IsOperand(char C)
{
	if (C >= '0' && C <= '9') return true;
	if (C >= 'a' && C <= 'z') return true;
	if (C >= 'A' && C <= 'Z') return true;
	return false;
}

// Check if character is a valid operator
bool IsOperator(char C)
{
	if (C == '+' || C == '-' || C == '*' || C == '/' || C == '$')
		return true;

	return false;
}

// Check right-associativity (e.g., exponent '$')
int IsRightAssociative(char op)
{
	if (op == '$') return true;
	return false;
}

// Return operator precedence weight
int GetOperatorWeight(char op)
{
	int weight = -1;
	switch (op)
	{
	case '+':
	case '-':
		weight = 1;
		break;
	case '*':
	case '/':
		weight = 2;
		break;
	case '$':
		weight = 3;
		break;
	}
	return weight;
}

// Compare precedence between two operators
int HasHigherPrecedence(char op1, char op2)
{
	int op1Weight = GetOperatorWeight(op1);
	int op2Weight = GetOperatorWeight(op2);

	if (op1Weight == op2Weight)
	{
		if (IsRightAssociative(op1)) return false;
		else return true;
	}
	return op1Weight > op2Weight ? true : false;
}
