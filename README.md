# MATLAB-CODE-Non-Linear-Function
function Nonlinear()

f = @(x) x^3 - x - 2;      % Main function (প্রশ্নে যে ফাংশনটা দেওয়া থাকবে)
df = @(x) 3*x^2 - 1;       % Derivatve form (Newton method)

% Parameters : 
%a = 1; 
%b = 2;
%x0 = 1.5;                  % Newton-Raphson initial guess
%tol = 1e-6;
%max_iter = 100;

% তোমরা এখানে সব গুলো ভ্যালু ইনপুট হিসেবেও নিতে পারো ভিন্ন ভিন্ন ফাংশনের জন্য:
a = input('Enter the value of a: ');
b = input('Enter the value of b: ');
x0 = input('Enter the value of x0: ');
tol = input('Enter the value of tol: ');
max_iter = input('Enter the max_iter: ');



% Run Methods: এর মানে ডিসপ্লে তে কিভাবে শো করবে সেটা।
% আগে মেথডের নাম প্রিন্ট হবে তারপর রুট বা রেজাল্ট দেখাবে। 

fprintf('\n --- Bisection Method --- \n');
bisection(f, a, b, tol, max_iter);

fprintf('\n --- Regular Falsi Method --- \n');
regular_falsi(f, a, b, tol, max_iter);

fprintf('\n --- Newton-Raphson Method --- \n');
newton_raphson(f, df, x0, tol, max_iter);




% Bisection Method
function root = bisection(f, a, b, tol, max_iter)
    if f(a)*f(b) > 0
        error('f(a) and f(b) must have opposite signs.');
    end
    for i = 1:max_iter
        c = (a+b)/2;
        if abs(f(c)) < tol || abs(b-a) < tol
            fprintf('Root found at x = %.6f after %d iterations\n', c, i);
            root = c;
            return;
        end
        if f(a)*f(c) < 0
            b = c;
        else
            a = c;
        end
    end
    root = (a+b)/2;
    fprintf('Root approx at x = %.6f after max iterations\n', root);
end





% Regular Falsi Method 
function root = regular_falsi(f, a, b, tol, max_iter)
    if f(a)*f(b) > 0
        error('f(a) and f(b) must have opposite signs.');
    end
    for i = 1:max_iter
        c = (a*f(b) - b*f(a)) / (f(b) - f(a));
        if abs(f(c)) < tol
            fprintf('Root found at x = %.6f after %d iterations\n', c, i);
            root = c;
            return;
        end
        if f(a)*f(c) < 0
            b = c;
        else
            a = c;
        end
    end
    root = (a*f(b) - b*f(a)) / (f(b) - f(a));
    fprintf('Root approx at x = %.6f after max iterations\n', root);
end





% Newton-Raphson Method 
function root = newton_raphson(f, df, x0, tol, max_iter)
    x = x0;
    for i = 1:max_iter
        fx = f(x);
        dfx = df(x);
        if dfx == 0
            error('Derivative became zero. Stopping...');
        end
        x_new = x - fx/dfx;
        if abs(f(x_new)) < tol
            fprintf('Root found at x = %.6f after %d iterations\n', x_new, i);
            root = x_new;
            return;
        end
        x = x_new;
    end
    root = x;
    fprintf('Root approx at x = %.6f after max iterations\n', root);
end
end
