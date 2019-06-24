<div class="name">
<div class="headings">Enter the table name</div>
<input type="text" bind:value={tb_name} placeholder="Table name" />
<div class="headings">Enter the operator</div>
<select name="op_type" bind:value={op_type}>
<option value="logical">Logical operator</option>
<option value="comparision">Comparision operator</option>
</select>
{#if op_type=="comparision"}
<div class="headings">Enter the operator name</div>
<select name="comparision_operator_name" bind:value={op_name}>
<option value="gt">Greater than</option>
<option value="lt">Less than</option>
</select>
<div class="headings">
<input type="text" bind:value={att} placeholder="attribute name" />
<input type="number" bind:value={val} placeholder="value" />
</div>

<button class="button" on:click={query_build}>Generate comparision query</button>
{#if tb_name=="" && lo_op_name==""}
<p>Query= {`db.${tb_name}.find({${att}: { $${op_name}: ${val}})`}</p>
{:else }Enter required values
{/if}
{:else if op_type=="logical"}
<select name="lo_op_name" bind:value={lo_op_name}>
<option value="and">AND</option>
<option value="not">NOT</option>
<option value="nor">NOR</option>
<option value="or">OR</option>
</select>
<input type="text" bind:value={att} placeholder="attribute name" />
<input type="number" bind:value={val} placeholder="value" />
<select name="comparision_operator_name" bind:value={op_name}>
<option value="gt">Greater than</option>
<option value="lt">Less than</option>
</select>
<button class="button1" on:click={push}>Push</button>

<button class="button" on:click={lo_query}>Generate logical query</button>
{#if tb_name=="" && lo_op_name=="" && lo==[]}
<p>Query= {`db.${tb_name}.find({ $${lo_op_name}: [ ${lo} } ]})`}</p>
{:else }Enter required values
{/if}
{:else}Invalid operator type entered

{/if}

</div>
<script>
let tb_name="",op_name="",att="",val=0,op_type="",lo=[],lo_op_name="";

function query_build(i){
console.log(`db.${tb_name}.find({${att}: { $${op_name}: ${val}})`)
}
function lo_query(){
    console.log(`db.${tb_name}.find({ $${lo_op_name}: [ ${lo} } ]})`)
}
function push(i){
    lo.push("{ "+op_name+": { $"+att+":"+val+" }}");
    lo=lo;
   }

</script>

<style>
    
p{
    color : red;
}
.name{
    color: rgb(107, 15, 15)
}
.headings{
    color: coral
    padding 10px
    }
.button {
  border: none;
  background-color: #4CAF50;
  padding: 10px 20px;
  color: aliceblue;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  border-radius: 12px;
  transition-duration: 0.4s;
}
.button:hover {
  background-color: #4CAF50; /* Green */
  color: white;
  }
.button1 {
  background-color: rgb(90, 83, 190);
  border: none;
  color: aliceblue;
  padding: 8px 15px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 12px;
  border-radius: 6px;
  }
</style>
