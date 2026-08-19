/**
 * @file infix_to_postfix.cpp
 * @brief Converts an Infix mathematical expression to Postfix notation (Reverse Polish Notation).
 * 
 * Objectives:
 * - Convert human-readable infix expressions (e.g., A + B * C) to postfix (e.g., A B C * +).
 * - Handle operator precedence and associativity (Left-to-Right vs Right-to-Left).
 * - Manage sub-expressions using opening and closing parentheses `()`.
 * 
 * Supported Operators:
 * - Addition (+), Subtraction (-) : Precedence 1 (Left-associative)
 * - Multiplication (*), Division (/) : Precedence 2 (Left-associative)
 * - Exponentiation ($) : Precedence 3 (Right-associative)
 * 
 * Time Complexity: O(n) where n is the length of the input expression.
 * Space Complexity: O(n) to store operators in the stack and build the output string.
 */

#include <iostream>
#include <stack>
#include <string>

// Function prototypes
std::string infixToPostfix(const std::string &expression);
bool hasHigherPrecedence(char op1, char op2);
bool isOperator(char ch);
bool isOperand(char ch);
bool isRightAssociative(char op);
int getOperatorWeight(char op);

int main() {
    std::string expression;
    std::cout << "Enter Infix Expression: ";
    std::getline(std::cin, expression);

    std::string postfix = infixToPostfix(expression);
    std::cout << "Postfix Output: " << postfix << "\n";

    return 0;
}

// Converts an infix expression string to a postfix expression string
std::string infixToPostfix(const std::string &expression) {
    std::stack<char> s;
    std::string postfix = "";

    for (char ch : expression) {
        // Skip spaces and commas used as delimiters
        if (ch == ' ' || ch == ',') {
            continue;
        }

        // If character is an operator (+, -, *, /, $)
        if (isOperator(ch)) {
            while (!s.empty() && s.top() != '(' && hasHigherPrecedence(s.top(), ch)) {
                postfix += s.top();
                s.pop();
            }
            s.push(ch);
        }
        // If character is an operand (letter or digit)
        else if (isOperand(ch)) {
            postfix += ch;
        }
        // If opening parenthesis, push onto the stack
        else if (ch == '(') {
            s.push(ch);
        }
        // If closing parenthesis, pop and append until matching '(' is found
        else if (ch == ')') {
            while (!s.empty() && s.top() != '(') {
                postfix += s.top();
                s.pop();
            }
            if (!s.empty()) {
                s.pop(); // Remove '(' from stack
            }
        }
    }

    // Pop and append any remaining operators in the stack
    while (!s.empty()) {
        postfix += s.top();
        s.pop();
    }

    return postfix;
}

// Checks if a character is an alphanumeric operand
bool isOperand(char ch) {
    if (ch >= '0' && ch <= '9') return true;
    if (ch >= 'a' && ch <= 'z') return true;
    if (ch >= 'A' && ch <= 'Z') return true;
    return false;
}

// Checks if a character is a recognized mathematical operator
bool isOperator(char ch) {
    return (ch == '+' || ch == '-' || ch == '*' || ch == '/' || ch == '$');
}

// Checks if the operator is right-associative (e.g., Exponentiation)
bool isRightAssociative(char op) {
    return op == '$';
}

// Returns numeric precedence weight of an operator
int getOperatorWeight(char op) {
    switch (op) {
        case '+':
        case '-':
            return 1;
        case '*':
        case '/':
            return 2;
        case '$':
            return 3;
        default:
            return -1;
    }
}

// Determines if op1 has higher or equal precedence compared to op2
bool hasHigherPrecedence(char op1, char op2) {
    int op1Weight = getOperatorWeight(op1);
    int op2Weight = getOperatorWeight(op2);

    if (op1Weight == op2Weight) {
        // If equal precedence, give priority to the left-associative operator
        if (isRightAssociative(op1)) return false;
        return true;
    }

    return op1Weight > op2Weight;
}
