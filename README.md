## Goodbye, Object Oriented Programming

https://medium.com/@cscalfani/goodbye-object-oriented-programming-a59cda4c0e53

1, Kế thừa :
* Banana Monkey Jungle Problem 

<p align='center'>
<img src="https://raw.githubusercontent.com/ttlpta/ttlpta.github.io/master/imgs/1.png">
</p>


## Learn Enough React For The Interview

https://medium.com/bb-tutorials-and-thoughts/learn-enough-react-for-the-interview-f460a2fa3aeb

1, What is Declarative Programming
* Mô hình lập trình tập trung vào bạn làm ra cái gì hơn là bạn làm thế nào. 
VD : 

>
    const numbers = [1,2,3,4,5];

    // declarative programming
    const doubleWithDec = numbers.map(number => number * 2);

    console.log(doubleWithDec)

    // imperative programming
    const doubleWithImp = [];
    for(let i=0; i<numbers.length; i++) {
        const numberdouble = numbers[i] * 2;
        doubleWithImp.push(numberdouble)
    }

    console.log(doubleWithImp)

2, What is Functional Programming
* Functional Programming là một phần của lập trình declarative. Functions trong JS là những hàm bạn có thể save , truy xuất và pass các functions này trong application giống những các variable
* Một số nội dung đặc trưng cho functional đó là : Immutability, Pure Functions, Data Transformations, Higher-Order Functions, Recursion, Composition


## Improve Performance in React.js Using Hooks
1, useCallback (memoize function) : Khi gặp trường hợp render với vòng lặp : 
>
    handleClick = (id) => {
        alert(id);
    }

    {
        items.map((item, idx)) => {
            return (<p onClick={ () => handleClick(item.id) }>{idx}</p>)
        });
    }


Việc này sẽ dẫn đến những re-render không cần thiết. Ta có thể cải thiện bằng cách : 

>
    handleClick = (id) => {
        alert(id);
    }

    {
        items.map((item, idx)) => {
            return (<p onClick={ useCallback( () => handleClick(item.id), [item]) }>{idx}</p>)
        });
    }

2, useMemo (Expensive Computations) : Khi gặp những phép toán phức tạp trước khi render ra view. Việc sử dụng useMemo sẽ giúp cache lại kết quả của phép tính trc, tránh việc phải tự động tính toán lại. Sẽ tính toán lại khi items truyền vào thay đổi
>
    import React, { useMemo } from 'react';

    const Dropdown = ({ items, onClick }) => {
    const memoizedValue = useMemo(() => {
        // This code will only run on initial render
        // and when "items" changes
        return items
        .filter(item => item < 5)
        .map(item => item + 3);
    }, [items]);
    
    return (...); // Returns some JSX
    }

## How to reuse react hooks
https://blog.bitsrc.io/simple-code-reuse-with-react-hooks-432f390696bf
>
    import { useState } from "react";

    export const useRandomColor = (colors, initialColor) => {
    const lenColors = colors.length;
    const [color, setColor] = useState(initialColor);

    const changeColor = () => {
        const index = Math.floor(Math.random() * lenColors);
        const pickedColor = colors[index];
        setColor(pickedColor);
    };

    return [color, changeColor];
    };


    // REUSE changeColor

    import React from "react";
    import { useRandomColor } from "./useRandomColor";

    export const ColoredBanner = () => {
        const colors = ["red", "blue", "green", "black"];
        const [color, changeColor] = useRandomColor(colors, "red");

        return (
            <div style={{
                textAlign: "center",
                padding: "20px 0",
                backgroundColor: color
            }} >
                <h2 style={{ color: "#fff" }}>Click below button to change Color</h2>
                <br />
                <button onClick={changeColor}>Change</button>
            </div>
            );
    };


## Top animation React
https://blog.bitsrc.io/11-javascript-animation-libraries-for-2018-9d7ac93a2c59

## Top JS library
https://blog.bitsrc.io/11-javascript-utility-libraries-you-should-know-in-2018-3646fb31ade


## Call vs Apply

Call và apply đều là để 1 function được viết thực hiện được ở 1 opject khác. Args thứ 1 là object sẽ thực hiện method đó , còn args thứ 2 là params truyền vào function . Khác nhau giữa call và apply là truyền mảng và truyền từng tham số

Hàm call
>   
    var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
    var person2 = {firstName: 'Kelly', lastName: 'King'};

    function say(greeting1, greeting2) {
        console.log(greeting1 + ',' + greeting2 + ' ' + this.firstName + ' ' + this.lastName);
    }

    say.call(person1, 'Hello', 'Good morning'); // => Hello,Good morning Jon Kuperman
    say.call(person2, 'Hello', 'Good morning'); // => Hello,Good morning Kelly King


Hàm Apply 
> 
    var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
    var person2 = {firstName: 'Kelly', lastName: 'King'};

    function say(greeting0, greeting1) {
        console.log(greeting0 + ',' + greeting1 + ' ' + this.firstName + ' ' + this.lastName);
    }

    say.apply(person1, ['Hello', 'Good moring']); // => Hello,Good moring Jon Kuperman
    say.apply(person2, ['Hello', 'Good moring']); // => Hello,Good moring Kelly King


Hàm Bind
>  
    var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
    var person2 = {firstName: 'Kelly', lastName: 'King'};

    function say(greeting0, greeting1) {
        console.log(greeting0 + ',' + greeting1 + ' ' + this.firstName + ' ' + this.lastName);
    }

    var sayHelloJon = say.bind(person1, 'Hello', 'Good morning');
    var sayHelloKelly = say.bind(person2, 'Hello', 'Good morning');

    sayHelloJon(); // => Hello,Good morning Jon Kuperman
    sayHelloKelly(); // => Hello,Good morning Kelly King

## Using the DOM like a Pro
To select a single element using any valid CSS selector use:
>
    document.querySelector('.foo')            // class selector
    document.querySelector('#foo')            // id selector
    document.querySelector('div')             // tag selector
    document.querySelector('[name="foo"]')    // attribute selector
    document.querySelector('div + p > span')  // you go girl!

Multiple elements
>
    document.querySelectorAll('p')  

Tips for making selector like Jquery
>
    const $ = document.querySelector.bind(document);
    $('#container');
    const $$ = document.querySelectorAll.bind(document);
    $$('p');

Going up the DOM tree
>
    document.querySelector('p').closest('div').closest('.content');

Adding elements
>
    const link = document.createElement('a');
    a.setAttribute('href', '/home');
    a.className = 'active';
    a.textContent = 'Home';
    document.body.appendChild(link);
Moving elements
>
    <!-- beforebegin -->
    <p>
    <!-- afterbegin -->
    foo
    <!-- beforeend -->
    </p>
    <!-- afterend -->
>
    <div class="first">
        <h1>Title</h1>
    </div>
    <div class="second">
        <h2>Subtitle</h2>
    </div>

and the h2 is inserted after the h1:
>
    const h1 = document.querySelector('h1');
    const h2 = document.querySelector('h2');
    h1.insertAdjacentElement('afterend', h2)

MutationObserver : Watch element when its attributes change

https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver
>
    // Select the node that will be observed for mutations
    const targetNode = document.getElementById('some-id');

    // Options for the observer (which mutations to observe)
    const config = { attributes: true, childList: true, subtree: true };

    // Callback function to execute when mutations are observed
    const callback = function(mutationsList, observer) {
        for(let mutation of mutationsList) {
            if (mutation.type === 'childList') {
                console.log('A child node has been added or removed.');
            }
            else if (mutation.type === 'attributes') {
                console.log('The ' + mutation.attributeName + ' attribute was modified.');
            }
        }
    };

    // Create an observer instance linked to the callback function
    const observer = new MutationObserver(callback);

    // Start observing the target node for configured mutations
    observer.observe(targetNode, config);

    // Later, you can stop observing
    observer.disconnect();