/**
 * @file balanced_parentheses.cpp
 * @brief Solution to check for balanced parentheses/brackets in an expression using a Stack.
 * 
 * Objectives:
 * - Validate nested brackets `()`, `{}`, and `[]` in mathematical/code expressions.
 * - Demonstrate a classic real-world application of the LIFO (Stack) property.
 * 
 * Algorithm:
 * - Push opening brackets onto the stack.
 * - For closing brackets, check if the stack is empty or if the top does not match the pair.
 * - An expression is balanced if the stack is completely empty at the end.
 * 
 * Time Complexity: O(n) where n is the length of the string.
 * Space Complexity: O(n) in the worst case where all characters are opening brackets.
 */

#include <iostream>
#include <stack>
#include <string>

// Helper function to check if the open and close characters form a valid pair
bool arePair(char open, char close) {
    if (open == '(' && close == ')') return true;
    if (open == '{' && close == '}') return true;
    if (open == '[' && close == ']') return true;
    return false;
}

// Function to check if the given expression contains balanced brackets
bool areBalanced(const std::string &exp) {
    std::stack<char> s;

    for (char ch : exp) {
        // Push opening brackets onto the stack
        if (ch == '(' || ch == '{' || ch == '[') {
            s.push(ch);
        }
        // Validate closing brackets against the top of the stack
        else if (ch == ')' || ch == '}' || ch == ']') {
            if (s.empty() || !arePair(s.top(), ch)) {
                return false;
            }
            s.pop();
        }
    }

    // If the stack is empty, all brackets were properly matched
    return s.empty();
}

int main() {
    std::string expression;
    std::cout << "Enter an expression: ";
    std::cin >> expression;

    if (areBalanced(expression)) {
        std::cout << "Balanced\n";
    } else {
        std::cout << "Not Balanced\n";
    }

    return 0;
}
