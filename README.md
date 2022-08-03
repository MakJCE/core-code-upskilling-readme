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
