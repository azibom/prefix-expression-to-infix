# prefix-expression-to-infix
prefix expression to infix


# what is prefix expression ?
Prefix : An expression is called the prefix expression if the operator appears in the expression before the operands. Simply of the form (operator operand1 operand2).
Example : *+AB-CD (Infix : (A+B) * (C-D) )

### now look at the code to find it how can you convert it :)

```cpp

#include <iostream> 
using namespace std; 

class Stack {
   protected:
      int top=-1;
      int MAX = 1000;
      string stack[1000];
   
   public:
      void push(string val) {
        if(top>=MAX-1)
            cout<<"Stack Overflow"<<endl; 
        else {
            top++;
            stack[top]=val;
        }
      }

      void pop() {
        if(top<=-1) {
            cout<<"Stack Underflow"<<endl;
        } else {
            top--;
        }
      }

      void display() {
        if(top>=0) {
            cout<<"Stack elements are:";
            for(int i=top; i>=0; i--)
                cout<<stack[i]<<" ";
                cout<<endl;
        } else
            cout<<"Stack is empty";
      }

      string get(int i) {
          return stack[i];
      }

      int getMax() {
          return MAX;
      }

      int getTop() {
          return top;
      }

      string getTopValue() {
          return stack[top];
      }

      int getSize() {
          return (top + 1);
      }

      int isEmpty() {
          if(top<=-1) return 1;
          return 0;
      }
};
  
bool isOperator(char x) { 
  switch (x) { 
  case '+': 
  case '-': 
  case '/': 
  case '*': 
  case '^': 
    return true; 
  } 
  return false; 
} 
  
string preToInfix(string pre_exp) { 
  Stack s; 
  int length = pre_exp.size(); 
  for (int i = length - 1; i >= 0; i--) { 
    if (isOperator(pre_exp[i])) { 
      string op1 = s.getTopValue();
      s.pop(); 
      string op2 = s.getTopValue();
      s.pop(); 
      string temp = "(" + op1 + pre_exp[i] + op2 + ")"; 
      s.push(temp);
    } 
    else { 
      s.push(string(1, pre_exp[i])); 
    } 
  } 
  return s.getTopValue(); 
} 
  
int main() { 
  string input; 
  cout << "Type a prefix expression: ";
  cin >> input;
  cout << "Infix is : " << preToInfix(input)<<endl; 
  return 0; 
} 

```
