
 * Objective: Check if an expression has balanced parentheses/brackets using a Stack.
 * Logic: Push opening brackets '(', '{', '[' and match/pop when closing brackets ')', '}', ']' appear.
 * Time Complexity: O(n) where n is the length of the string
 * Space Complexity: O(n)


#include<iostream>
#include<stack>
#include<string>
using namespace std;

// Check if open and close brackets match
bool ArePair(char open, char close)
{
	if (open == '(' && close == ')') 
		return true;
	else if (open == '{' && close == '}') 
		return true;
	else if (open == '[' && close == ']') 
		return true;
	return false;
}

// Function to verify if expression is balanced
bool AreBalanced(string exp)
{
	stack<char> S;
	int length = exp.length();

	for (int i = 0; i < length; i++)
	{
		// Push opening brackets to stack
		if (exp[i] == '(' || exp[i] == '{' || exp[i] == '[')
			S.push(exp[i]);

		// For closing brackets, check matching top element
		else if (exp[i] == ')' || exp[i] == '}' || exp[i] == ']')
		{
			if (S.empty() || !ArePair(S.top(), exp[i]))
				return false;
			else
				S.pop();
		}
	}
	// If stack is empty, all brackets are balanced
	return S.empty();
}

int main()
{
	string expression;
	cout << "Enter an expression: ";
	cin >> expression;

	if (AreBalanced(expression))
		cout << "Balanced\n";
	else
		cout << "Not Balanced\n";

	return 0;
}
