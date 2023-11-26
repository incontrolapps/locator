<script>
import monica from "../data/monicaMaker"
let myMonica=null;

let selection={
    "S1":null,
    "B1": null,
    "I1":null,
    "I2":null,
    "B2": null,
    "B3": null,
    "I3":null,   
    "B4": null,   
    "B5": null,     
    "I4": null
}

if (typeof window !== 'undefined') {
    if (localStorage.getItem("selection")){selection=JSON.parse(localStorage.getItem("selection"))}
    else{ 
        selection.S1=monica;
}
localStorage.setItem("selection",JSON.stringify(selection))
}

function capitalise(str) {
  return str.replace(
    /\w\S*/g,
    function(txt) {
      return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase();
    }
  );
}

let completed=0;

function post(data){
    
}

function saveSelection(selection){

localStorage.setItem("selection",JSON.stringify(selection))
Object.values(JSON.parse(localStorage.getItem("selection"))).filter(e=>e==null).length==0?completed=1:console.log("selection",selection);
}

let accomplished=false

$: typeof window !== 'undefined' && selection && saveSelection(selection)

</script>

{#if typeof window !== 'undefined'}

<h1>Impact survey of the ONS hybrid working mandate on colleagues</h1>
<p>This is an anonymous survey with results made available automatically as responses come in. It is intended for staff at the ONS to aid their own understanding of the impacts of current changes on colleagues, and to help them put their own situations in context.</p>
<p>This survey is designed to keep participants anonymous. It will be conducted iteratively as <a href="/questions">new research questions are proposed</a>. No data will be stored beyond the answers to the questions and a timestamp.</p>
<p>Your unique monica is "<b style="color:#c64e08">{capitalise(selection.S1)}</b>"  Make a note of this in case you would like to continue to contribute to this survey in the future from a different browser or device or after clearing your browser history.</p>
<p><b>You will need to complete all nine initial questions to unlock the <a href="/results">survey results</a>.</b> Whenever you are up-to-date with your answers, the results will be freely available to you</p>
<br><br>
<b>Question 1:</b> Did you start working at the ONS before the Covid lockdowns?
<br><select id="B1" bind:value={selection.B1}><option value={1}>Yes</option><option value={0}>No</option></select>
<br>
<b>Question 2:</b> How long does it take you to travel to your designated office?
<br><select id="I1" bind:value={selection.I1}>
    <option value={10}>0 to 10 minutes</option>
    <option value={20}>10 to 20 minutes</option>
    <option value={30}>20 to 30 minutes</option>
    <option value={40}>30 to 40 minutes</option>
    <option value={50}>40 to 50 minutes</option>
    <option value={60}>50 to 60 minutes</option>   
    <option value={70}>over one hour</option>      
</select>
<br>
<b>Question 3:</b> Before Covid, whether you were at the ONS or not, how long did your one-way daily commute to work or study take?
<br><select id="I2" bind:value={selection.I2}>
    <option value={10}>0 to 10 minutes</option>
    <option value={20}>10 to 20 minutes</option>
    <option value={30}>20 to 30 minutes</option>
    <option value={40}>30 to 40 minutes</option>
    <option value={50}>40 to 50 minutes</option>
    <option value={60}>50 to 60 minutes</option>   
    <option value={70}>over one hour</option>      
</select>
<br>
<b>Question 4:</b> From January 2024, will you be able to easily use public transport, walk or cycle to your designated office?
<br><select id="B2" bind:value={selection.B2}><option value={1}>Yes</option><option value={0}>No</option></select>
<br>
<b>Question 5:</b> Are the majority of your close colleagues linked to the same office location as you?
<br><select id="B3" bind:value={selection.B3}><option value={1}>Yes</option><option value={0}>No</option></select>
<br>
<b>Question 6:</b> What level of formal qualifications do you have?
<br><select id="I3" bind:value={selection.I3}>
    <option value={1}> <b>No formal qualifications</b></option> 
    <option value={2}><b>Level 1:</b> one to four GCSE passes (grade A* to C or grade 4 and above) and any other GCSEs at other grades, or equivalent qualifications</option> 
    <option value={3}><b>Level 2:</b> five or more GCSE passes (grade A* to C or grade 4 and above) or equivalent qualifications</option> 
    <option value={4}><b>Level 3:</b> two or more A Levels or equivalent qualifications</option> 
    <option value={5}><b>Level 4:</b> Higher National Certificate, Higher National Diploma, Bachelor's degree</option>
    <option value={6}><b>Over level 4: Post-graduate qualifications</b></option> 
</select>
<br>
<b>Question 7:</b> Do you think your job requires skills that most office workers don't have and that take more than a year to learn?
<br><select id="B4" bind:value={selection.B4}><option value={1}>Yes</option><option value={0}>No</option></select>
<br>
<b>Question 8:</b> How long do you think a new recruit with the same skills and education as you would take to pick-up your job? 
<br><select id="B5" bind:value={selection.B5}>    
    <option value={1}>Up to one month</option> 
    <option value={2}>Up to three months </option> 
    <option value={3}>Up to six months</option> 
    <option value={4}>Up to one year</option> 
    <option value={4}>Over one year</option> 
</select>    
<br>
<b>Question 9:</b> Before the announcement of the new hybrid working arrangements, how satisfied were you with your job?
<br><select id="I4" bind:value={selection.I4}>
    <option value={1}><b>Highly dissatisfied</b></option>
    <option value={2}><b>Dissatisfied</b></option>
    <option value={3}><b>Neutral</b></option>
    <option value={4}><b>Satisfied</b></option>
    <option value={5}><b>Highly satisfied</b></option>
</select>
{/if}
{#if completed}
<div class="over"><div class="ready">ready to submit?</div>
<div class="accomplished" class:visble={accomplished}>
    <div class="submit">Submit and see other people's results</div>
    <div class="edit" on:click={()=>completed=0}>Edit before sending</div>
</div>
</div>
{/if}
<style>

    select{
        max-width: 400px;
        height: 30px;
        margin-top: 10px;
    }
    .accomplished{
        height: 80vh;
        width: 80vw;
        margin-left: 10vw;
        margin-top: 10vh;
        position: fixed;
        top: 0;
        left: 0;
        background-color:none;
        opacity: 0.9;
        color: black;
        border-radius: 50px;
        display: flex;
        justify-content: space-evenly;
        font-size: 50px;
        font-weight: bold;
    }
    .submit{
        padding: 10%;
        background-color: green;
        margin: 50px;

        border-radius: 20px;
        width: 30%;
        text-align: center;
    }
    .edit{
        padding: 10%;  
        background-color: orange;
        margin: 50px;

        border-radius: 20px;
        width: 30%;
        text-align: center;
    }
    .submit:hover{
       background-color: rgb(9, 80, 9);
    }
    .edit:hover{
        background-color: rgb(179, 120, 12);
    }
    .ready{
color: white;
    }
</style>