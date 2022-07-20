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
