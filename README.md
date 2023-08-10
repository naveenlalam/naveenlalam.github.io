## Welcome to GitHub Pages

## This is Naveen, I am a student of M.S. Applied Computer Science in Grand Valley State University

## Interests - Travel is my passion, I visited six countries in Asia Pacific region.Europe is next in travel list.

## Experience - Worked as a Software Engineer and have skills in J2EE technolgies, Azure Cloud and Web Technologies. 


[meme](http://www.quickmeme.com/meme/3ozepj)


## Term Project - University Messaging System 
   University Messaging System is a communication system that can be leveraged by all registered users of the university.
   Users will be able to send messages to people depending on there access level for e.g. President of the university will 
   have rights to send message to all the department heads, faculty and students as a group or to an individual.Users who 
   require access to system should register in the portal and after an approval the user would be able to login to the 
   application.

   [Project Details](https://naveenlalam.github.io/GVSU-CIS641-Panda/)


   import logo from './logo.svg';
import './App.css';
import * as XLSX from 'xlsx'; 
import React, { useState, useEffect } from 'react'; 

function App() {

  const [data1, setData1] = useState([]); 
  const [data2, setData2] = useState([]); 
  useEffect(() => { 
    // Fetch data from API 1 
     //fetch('https://tradestie.com/api/v1/apps/reddit')
    fetch('https://jsonplaceholder.typicode.com/albums/1/photos')
       .then(response => response.json()).then(data => setData1(data));
     // Fetch data from API 2 
     fetch('https://jsonplaceholder.typicode.com/todos')
        .then(response => response.json()).then(data => setData2(data)); }, []); 
     const handleExport = () => { 
      
      const wb = XLSX.utils.book_new(); 
      // Create worksheet for combined data with space between tables 
      const combinedData = [data1[0],...data1, {}, {}, {}, {}, {}, data2[0],...data2]; 

      console.log(data1);
console.log(data2);
      //const ws = XLSX.utils.json_to_sheet(combinedData); 

      const ws = XLSX.utils.json_to_sheet(combinedData); 


       //const wv = XLSX.utils.json_to_sheet([],{header: Object.keys(data2[0])}); 




      XLSX.utils.book_append_sheet(wb, ws, 'Combined Data'); 



      //XLSX.utils.book_append_sheet(wb, wv, 'Table 2'); 



      const wbout = XLSX.write(wb, { bookType: 'xlsx', type: 'binary' }); 
      const blob = new Blob([s2ab(wbout)], 
      { type: 'application/octet-stream' }); 
      const fileName = 'combined_data.xlsx'; saveAs(blob, fileName); }; 
      
      const saveAs = (blob, fileName) => { 
        const link = document.createElement('a'); 
        link.href = URL.createObjectURL(blob); 
        link.download = fileName; link.click(); 
      }; 

      const s2ab = s => { 
        const buf = new ArrayBuffer(s.length); 
        const view = new Uint8Array(buf); 
        for (let i = 0; i !== s.length; ++i) 
            view[i] = s.charCodeAt(i) & 0xff; 
            return buf; 
        }; 


  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
       
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
        <button onClick={handleExport}>Export to Excel</button>
      </header>
    </div>
  );
}

export default App;
