# core-code-upskilling-readme

### Week 1 - Tuesday

*Ensure Question*

    function ensureQuestion(str){

       return str[str.length-1] === '?'? str : str+'?';

    }

*Reverse Words*

    function reverseWords(str){

      return str.split(' ').reverse().join(' ');

    }
    
### Week 1 - Wednesday

*Find the smallest integer in the array*

    function smallestElement(arr){
      return arr.reduce((el1, el2)=> el1>el2? el2 : el1, arr.at(0));
    }
    
### Week 1 - Thursday

*Odd or Even?*
    
    function oddOrEven(array) {
      if(array.length === 0) return 'even';
      let sum = array.reduce((el1, el2)=> el1+el2, 0);
      return sum%2===0?'even':'odd';
    }

### Week 2 - Monday

*Palindrome Strings*
    
    function isPalindrome(line) {
      if(typeof line === 'number') line = line.toString();
      return line === line.split('').reverse().join('');
    }    

### Week 2 - Tuesday

*Well of Ideas - Easy Version*

    function well(x){
      var countGoods = x.reduce((el1, el2)=>(el2==='good')?el1+1:el1, 0);
      return countGoods===0? 'Fail!' : countGoods < 3? 'Publish!' : 'I smell a series!';
    }

### Week 2 - Wednesday

*Managing Events in React JS*

    import React from 'react';

    export class Counter extends React.Component {
      constructor(props) {
        super(props);
        this.state = {counter: 0};
      }

      // Your event handlers 
      render() {
        return (
          <div>
            <h1 id="counter">{this.state.counter}</h1>
              <button type="button" id="decrement" onClick={()=>{this.state.counter -= 1;}}>
                Decrement
              </button>
              <button type="button" id="increment" onClick={()=>{this.state.counter += 1;}}>
                Increment
              </button>
          </div>
        )
      }
    }

### Week 2 - Thursday

*Santa wish list form in ReactJS*

    const React = require("react");

    class WishlistForm extends React.Component {
      constructor(props) {
        super(props);
        this.state = {wish:'', name:'', priority:1};
      }

      render() {
        const handleSubmit = (event)=>{
          this.props.send(this.state);
          event.preventDefault();
        }
        const handleOnChange = (event, key) =>{
          this.state[key] = event.target.value;
        }
        return (
          <form >
            <input id="name" name="name" type="text" onChange={(event)=>handleOnChange(event, 'name')}/>
            <textarea id="wish" name="wish" onChange={(event)=>handleOnChange(event, 'wish')}></textarea>
            <select id="priority" name="priority" value={1} onChange={(event)=>handleOnChange(event, 'priority')}>
              <option value={1}>1</option>
              <option value={2}>2</option>
              <option value={3}>3</option>
              <option value={4}>4</option>
              <option value={5}>5</option>
            </select>
            <input type="submit" value="Submit"/>
          </form>
        );
      }
    };

*PC upgrade specs using HOC in ReactJS*

    const React = require('react');

    // Don't change PcDisplay
    const PcDisplay = (props) => {
      console.log("sa", props.price);
      return (<div>
      <h1>{props.title}</h1>
      <p id="price">£{props.price}</p>
      <ul>
        <li><label>CPU</label> <span>{props.cpu}</span></li>
        <li><label>RAM</label> <span>{props.ram}</span></li>
        <li><label>SSD</label> <span>{props.ssd}</span></li>
      </ul>
      </div>);
    };

    // Implement HOC -> returns a functions that wraps the passed in `PcDisplay` component
    let withPriceModel = (Component, model)=>{
      return (props)=>{
        props.price = model === 'basic'? 50: model === 'pro'? 110: 50;
        return(
        <Component {...props} />
      )};
    };

    // Build basic and pro model components using `withPriceModel`
    let BasicModel=(props)=>{return withPriceModel(PcDisplay, 'basic')(props)};

    let ProModel=(props)=>{return withPriceModel(PcDisplay, 'pro')(props)};
    
### Week 3 - Monday

*Search filter in React*

    function SearchList() {
      const defaultList = [
        "Banana",
        "Apple",
        "Orange",
        "Mango",
        "Pineapple",
        "Watermelon",
      ];

      const [list, setList] = useState(defaultList);

      const handleSearch = (event) => {
        if (event.target.value === "") {
          setList(defaultList);
          return;
        }
        setList(defaultList.filter( (item) => item.toLowerCase().includes(event.target.value) );
      };
      return (
        <div className="app">
          <div>
            Search: <input name="query" type="text" onChange={handleSearch} />
          </div>
          {list &&
            list.map((item) => (
              <div>{item}</div>
            ))}
        </div>
      );
    }

    export default SearchList;

### Week 3 - Tuesday

*Fetch Random User Data*

    import React, { useState, useEffect } from 'react';

    function RandomUser() {
      const [userData, setUserData] = useState({});

      const getUserData = () => {
        const random = Math.floor(Math.random() * 10) + 1;
        fetch(`https://jsonplaceholder.typicode.com/users/${random}`)
          .then((response) => {
            response.json().then(jsonResponse => {setUserData(jsonResponse);})
          })
          .catch((error) => {
            console.error(error);
          });
      };

      useEffect(() => {
        getUserData();
      }, []);

      return (
        <div className="App">
          <button onClick={getUserData}>Reset</button>
          <h1>User Data</h1>

          <div>
            <b>Name:</b> {userData.name}
          </div>
          <div>
            <b>Website:</b> {userData.website}
          </div>
          <div>
            <b>Email:</b> {userData.email}
          </div>
          <div>
            <b>Phone:</b> {userData.phone}
          </div>
        </div>
      );
    }

    export default RandomUser;

### Week 3 - Wednesday

*React Router Blog*

    //index.js
    root.render(
      <BrowserRoute>
        <Routes>
          <Route path="/" element={<App />}/>
          <Route path="/:id" element={<Blog />}/>
        </Routes>
      </BrowserRoute>
    );
    
    //App.js
    export default function App() {
      const [blogs, setBlogs] = useState([]);
      useEffect(() => {
        fetch("blogs.json")
          .then((response) => {
            response.text();
          })
          .then((resp) => {
            setBlogs(JSON.parse(resp));
          });
      }, []);
      return (
        <div className="App">
          <h1>Most Awesome Blogs</h1>
          {blogs.map((blog) => {
            return <Link to={blog.id}>{blog.title}</Link>;
          })}
        </div>
      );
    }
    
    //Blog.js
    const Blog=()=>{
      const {id} = useParams();
      const [blog, setBlog] = useState();
      useEffect(() => {
        fetch(`blogs.json`)
        .then(response => response.text())
        .then(data => {
            data = JSON.parse(data);
            console.log(data);
            setBlog(data.find(b=> b.id === id));
        });
      }, [id]);
      return(
        <div>
          <h1>{blog.title}</h1>
          <p>{blog.content}</p>
          <p>{blog.author}</p>
        </div>
      );
    }

### Week 4 - Moonday

*Two to One*

    function longest(s1, s2) {
      let setOfList = new Set(s1.concat(s2).split(''))
      let sortedList = Array.from(setOfList).sort((a,b)=>{
        if(a<b) return -1;
        if(a>b) return 1;
        return 0;
      });
      return (sortedList.join(''));
    }

### Week 4 - Tuesday

*Leap Day*

     function isLeapYear(year) {
      const div4 = year%4 === 0;
      const div100 = year%100 === 0;
      const div400 = year%400 === 0;
      if (div4){
        if(div100){
          if(div400) return true;
          return false;
        }
        return true;
      }
      return false;
    }

### Week 4 - Wednesday

*Maximum Length Difference*

     function mxdiflg(a1, a2) {
        if(a1.length===0 || a2.length===0) return -1;
        const maxAndMin = (s1,s2, operation)=>{ 
         if(operation==='max') 
           return(s1.length>s2.length)?s1:s2; 
         return(s1.length<s2.length)?s1:s2;
        };
        const findMaxMinLength = 
              (arr)=> arr.reduce(
                (e1,e2)=>[maxAndMin(e1[0], e2, 'max'), maxAndMin(e1[1], e2, 'min')]
              , [arr[0], arr[0]]);
        const [maxa1, mina1] = findMaxMinLength(a1);
        const [maxa2, mina2] = findMaxMinLength(a2);
        return Math.max(maxa1.length-mina2.length , maxa2.length-mina1.length);
    }

### Week 4 - Thursday

*Base64 Numeric Translator*

    function base64toBase10(base64) {
      const sequence = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/";
      const digits = {};
      for(let i in sequence.split('')){
        digits[sequence[i]] = parseInt(i);
      }
      var resp=0;
      const reverseBase64 = base64.split('').reverse();
      for(let i in reverseBase64) {
        resp+=digits[reverseBase64[i]]*Math.pow(64,i);
      }
      return resp;
    }

### Week 5 - Monday

*Fun with lists: map*

    function map(head, f) {
      if(!head) return null;
      var newHead = head;
      while (!!newHead){
        newHead.data = f(newHead.data);
        newHead=newHead.next;
      }
      return head;
    }
    
### Week 5 - Tuesday

*Separating String*

    function sepStr(str) {
      var resp = [];
      var words = str.split(' ');
      var rows = words.reduce((w1,w2)=>w1.length>w2.length?w1:w2).length;
      var cols = words.length;
      let row = 0;
      while( row < rows){
        resp.push([]);
        for(let word of words){
          resp[row].push(word[row] || '');
        }
        row+=1;
      }
      return resp;
    }
    
### Week 5 - Wednesday

*Highest Scoring Word*

    function high(x){
      const getScore = (word)=>{
        return word.split('').reduce((total,ls)=> total+(ls.charCodeAt(0)-96),0);
      }
      return x.split(' ').reduce((w1, w2)=> (getScore(w1)>=getScore(w2))?w1:w2);
    }

### Week 5 - Thursday

*Where Is My Parent?*

    function findChildren(dancingBrigade) {
        return dancingBrigade.split('').sort((a,b)=>{
        let code1 = a.charCodeAt(0);
        code1 = code1<97? code1 + 31.5 : code1;
        let code2 = b.charCodeAt(0);
        code2 = code2<97? code2 + 31.5 : code2;
        return code1-code2;
      }).join('');
    }

### Week 6 - Monday

*Expressions Matters*

    SELECT CASE 
    WHEN (a=1) AND (c=1) THEN a + b + c
    WHEN (a=1) OR ((b=1) AND (a < c)) THEN (a + b) * c
    WHEN (c=1) OR ((b=1) AND (a>=c)) THEN a * (b + c)
    ELSE a*b*c
    END AS res
    FROM expression_matter;

### Week 6 - Tuesday

*Sudoku Solution Validator*

    function validSolution(board){
      var digits = [];
      for(let i=0; i<10; i++){digits.push({rows: new Set(), cols: new Set()})}

      for(let i in board){
        for(let j in board[i]){
          if(digits[board[i][j]]){
           digits[board[i][j]].rows.add(i);
           digits[board[i][j]].cols.add(j);
          }
        }
      }
      var resp = true;
      if(!!digits[0] && (digits[0].rows.size >0 || digits[0].cols.size > 0)) return false;
      for(let i=1; i<10; i++){
        let dig = digits[i];
        if(dig){
         if(dig.rows.size !== 9 || dig.cols.size !== 9){
            resp = false;
            break;
            }
        }
      }
      return resp;
    }

### Week 6 - Wednesday

*Even or Odd*

    SELECT CASE 
    WHEN number%2 = 0 THEN 'Even'
    ELSE 'Odd'
    END AS is_even
    FROM numbers;

### Week 6 - Thursday

*Returning Strings*

    SELECT format('Hello, %s how are you doing today?', name) as greeting FROM person

### Week 7 - Monday

*Simple NULL handling*

    SELECT 
    id, 
    CASE WHEN name = '' THEN COALESCE('[product name not found]') ELSE name END as name,
    price,
    CASE WHEN card_name = '' THEN NULLIF('[card name not found]','') ELSE card_name END as card_name,
    card_number, 
    transaction_date 
    FROM eusales
    WHERE price >= 50

### Week 7 - Tuesday

*The takeWhile Function*

    function takeWhile (arr, pred) {
      let validPred = true;
      return arr.reduce((one, two)=>{
        if(validPred){
          validPred = pred(two);
          return validPred? [...one, two]: one;
        }else{
          return one;
        }
      }, [])
    }

### Week 7 - Wednesday

*The Supermarket Queue*

    function queueTime(customers, n) {
      if(customers.length === 0) return 0;
      var queues = customers.slice(0,n);
      let rest = customers.slice(n, customers.length);
      for(let c of rest){
        queues.sort();
        queues[0]+=c;
      }
      queues.sort();
      return queues[queues.length-1];
    }
    
### Week 7 - Thursday

*Sum Of Digits / Digital Root*

    function digitalRoot(n) {
      var fun = (cad)=>cad.reduce((uno,dos)=>parseInt(uno)+parseInt(dos), 0);
      var sn = String(n);
      var suma = fun(sn.split(''));
      if(String(suma).length === 1) return suma;
      return digitalRoot(suma);
    }
    
### Week 8 - Links not working

### Week 9 - Monday

*Install a Kubernetes Local Cluster*

I've installed Docker Desktop

![alt text](https://i.ibb.co/jytzjNL/temp.png)


### Week 9 - Tuesday

![alt text](https://i.ibb.co/qpdhSs2/temp.png)


### Week 9 - Wednesday

![alt text](https://i.ibb.co/mRXwCFL/temp.png)

![alt text](https://i.ibb.co/5n6hdBw/temp.png)


### Week 9 - Thursday

![alt text](https://i.ibb.co/Dfzndz4/temp.png)

![alt text](https://i.ibb.co/n3d5TX6/temp.png)


### Week 10 - Monday 

*How to use the Google Cloud Free Program*

![alt text](https://i.ibb.co/WyF5pNw/temp.png)


### Week 10 - Tuesday - Not working links

