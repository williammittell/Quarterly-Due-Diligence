# Quarterly-Due-Diligence
Koda's ISG Quarterly Due Diligence
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Detailed Screening — Submission Portal</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Archivo+Narrow:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --teal-header:#00C7B5; --teal-header-dk:#00a89a; --teal-band:#0c5048;
    --teal-light:#E5F9F7; --yellow:#FFFFCC; --yellow-bright:#FFFF00; --pink:#FFCCFF;
    --red:#d11a1a; --grid:#bfbfbf; --grid-soft:#d9d9d9;
    --ink:#1a1a1a; --ink-soft:#555; --bg:#ffffff; --shell:#f3f3f1;
  }
  *{box-sizing:border-box;margin:0;padding:0}
  body{zoom:1.05;background:var(--shell);color:var(--ink);font-family:'Archivo Narrow','Aptos Narrow',Calibri,system-ui,sans-serif;font-size:13px;line-height:1.35;-webkit-font-smoothing:antialiased;padding:1.5rem 1rem 6rem}

  .layout{display:flex;gap:1.1rem;align-items:flex-start;max-width:1320px;margin:0 auto}

  .cat-index{position:sticky;top:1rem;width:218px;flex:none;background:var(--bg);border:1px solid var(--grid);border-radius:6px;box-shadow:0 6px 18px -12px rgba(0,0,0,.3);max-height:calc(100vh - 2rem);display:flex;flex-direction:column;overflow:hidden}
  .ci-head{background:var(--teal-band);color:#fff;font-weight:700;font-size:12px;letter-spacing:.06em;text-transform:uppercase;padding:.6rem .8rem}
  .ci-list{list-style:none;overflow-y:auto;padding:.3rem 0}
  .ci-list a{display:block;text-decoration:none;color:var(--ink-soft);font-size:12.5px;padding:.42rem .85rem .42rem .8rem;border-left:3px solid transparent;transition:background .12s,color .12s,border-color .12s;line-height:1.25}
  .ci-list a:hover{background:var(--teal-light);color:#08312c}
  .ci-list a.active{background:var(--teal-light);color:#08312c;border-left-color:var(--teal-header);font-weight:700}

  .sheet{flex:1;min-width:0;background:var(--bg);border:1px solid var(--grid);box-shadow:0 1px 0 rgba(0,0,0,.04),0 10px 30px -18px rgba(0,0,0,.35)}
  .sheet-tabs{display:flex;background:#e4e4e1;border-bottom:1px solid var(--grid);padding:.35rem .4rem 0}
  .tab{font-size:12px;font-weight:600;padding:.45rem .85rem;color:var(--ink-soft);background:#d6d6d3;margin-right:2px;border:1px solid transparent;border-bottom:none;border-radius:4px 4px 0 0;cursor:pointer;user-select:none}
  .tab:hover{background:#cdcdc9}
  .tab.active{background:var(--bg);color:var(--ink);border-color:var(--grid);cursor:default}
  .sheet-body{padding:1.4rem 1.4rem 1.8rem}

  .panel{display:none}
  .panel.active{display:block;animation:fade .18s ease}
  @keyframes fade{from{opacity:0}to{opacity:1}}

  .action-note{color:var(--red);font-weight:700;font-size:12px;letter-spacing:.02em;margin-bottom:.2rem}
  .action-note.info{color:var(--ink-soft)}
  .sheet-title{font-size:18px;font-weight:700;margin-bottom:1rem}
  .instruct{background:#fffceb;border:1px solid #ecd98a;border-radius:4px;padding:.6rem .8rem;font-size:12px;color:#5c4d12;margin-bottom:1.2rem;display:flex;gap:.5rem;align-items:flex-start}
  .instruct b{color:#3f3408}
  .config-banner{background:#fff3d6;border:1px solid #e0b84a;border-radius:4px;padding:.55rem .8rem;font-size:12px;color:#6b4d12;margin-bottom:1.1rem;display:flex;gap:.5rem;align-items:flex-start}
  .config-banner code{background:rgba(0,0,0,.07);padding:.05rem .3rem;border-radius:3px}

  /* Fund Details Q/A table */
  table.qa{border-collapse:collapse;width:100%;border:1px solid var(--grid)}
  table.qa th{background:var(--teal-header);color:#08312c;text-align:left;font-size:12px;font-weight:700;padding:.5rem .6rem;border:1px solid var(--teal-header-dk)}
  table.qa td{border:1px solid var(--grid-soft);vertical-align:top;padding:0}
  table.qa td.q{background:#fff;padding:.6rem .65rem;width:46%;font-size:12.5px;color:var(--ink);white-space:pre-line;line-height:1.4}
  table.qa td.a{background:var(--yellow);padding:0}
  table.qa td.a input,table.qa td.a select,table.qa td.a textarea{width:100%;border:none;background:transparent;font-family:inherit;font-size:12.5px;color:var(--ink);padding:.6rem .6rem}
  table.qa td.a textarea{min-height:64px;resize:vertical}
  table.qa td.a select{cursor:pointer}
  table.qa td.a input:focus,table.qa td.a select:focus,table.qa td.a textarea:focus{outline:2px solid var(--teal-header);outline-offset:-2px;background:#fff}
  .qa-sub{border-top:1px dashed var(--yellow-edge,#e2e29a)}

  /* Instructions */
  .instr-list{list-style:none;counter-reset:step;border:1px solid var(--grid);border-radius:4px;overflow:hidden}
  .instr-list li{padding:.6rem .8rem;font-size:12.5px;line-height:1.5;border-bottom:1px solid var(--grid-soft);background:#fff;white-space:pre-line}
  .instr-list li:last-child{border-bottom:none}
  .instr-list li b{color:#08312c}
  .instr-list a{color:var(--teal-header-dk)}
  .ex-title{font-weight:700;font-size:14px;margin:1.4rem 0 .6rem}

  /* Shared table */
  .table-scroll{overflow-x:auto;border:1px solid var(--grid)}
  table.grid{border-collapse:collapse;width:100%;min-width:1000px}
  table.grid thead th{background:var(--teal-header);color:#08312c;font-weight:700;font-size:12px;text-align:left;padding:.5rem .55rem;border:1px solid var(--teal-header-dk);white-space:nowrap}
  table.grid thead th .sub{display:block;font-weight:400;font-size:10.5px;color:#0a4a43}
  table.grid td{border:1px solid var(--grid-soft);padding:0;vertical-align:middle}

  tr.cat-band{scroll-margin-top:.6rem}
  tr.cat-band td{background:var(--teal-band);color:#fff;font-weight:700;font-size:13px;letter-spacing:.04em;text-transform:uppercase;padding:.5rem .6rem;border:1px solid var(--teal-band);white-space:pre-line;line-height:1.4}

  tr.act-head td{font-weight:700;font-size:12px}
  tr.act-head .toggle{background:var(--teal-light);color:#08312c;padding:.5rem .5rem;cursor:pointer;user-select:none;min-width:230px}
  tr.act-head .toggle:hover{background:#d8f4f0}
  .chev{display:inline-block;width:.85em;color:var(--teal-header-dk);transition:transform .15s;font-size:11px}
  tbody.group.open .chev{transform:rotate(90deg)}
  tr.act-head .dc-cell{background:var(--teal-light);padding:0;width:100px}
  tr.act-head .dc-cell select{width:100%;border:none;background:var(--yellow-bright);font-family:inherit;font-weight:700;font-size:12px;text-align:center;padding:.5rem .3rem;cursor:pointer;appearance:none}
  tr.act-head .dc-cell select:focus{outline:2px solid var(--teal-header);outline-offset:-2px}
  tr.act-head .head-label{background:var(--teal-light);color:#08312c;padding:.5rem .5rem}
  tr.act-head .head-label .hint{font-weight:400;color:#0a7367;font-style:italic}
  tr.act-head .head-total{background:var(--pink);text-align:right;padding:.5rem .55rem;font-variant-numeric:tabular-nums;width:90px;white-space:nowrap}
  tr.act-head .head-end{background:var(--teal-light)}

  tbody.group:not(.open) tr.data,
  tbody.group:not(.open) tr.adder{display:none}

  tr.data:hover td{background-color:rgba(0,199,181,.04)}
  td.activity-cell{background:var(--teal-light);min-width:230px;padding:.45rem .5rem .45rem 1.6rem;font-size:12px;color:#0a4a43}
  td.blankteal{background:var(--teal-light);width:100px}
  td.yellow{background:var(--yellow)}
  td.yellow input{width:100%;border:none;background:transparent;font-family:inherit;font-size:12.5px;color:var(--ink);padding:.45rem .5rem}
  td.yellow input::placeholder{color:#c4c489}
  td.num input{text-align:right}
  td input:focus{outline:2px solid var(--teal-header);outline-offset:-2px;background-color:#fff}
  td.actual{background:#fff;text-align:right;padding:.45rem .55rem;font-variant-numeric:tabular-nums;font-weight:600;width:90px;white-space:nowrap}
  td.holding{min-width:150px}
  td.comments{min-width:210px}
  td.rm{width:34px;text-align:center;background:#fafafa}
  td.rm button{border:none;background:none;color:#c2c2c2;font-size:15px;cursor:pointer;line-height:1;padding:.3rem .35rem;border-radius:3px}
  td.rm button:hover{color:var(--red);background:#fce8e8}

  tr.adder td{background:#fbfbf8;padding:.2rem .5rem;border-top:1px dashed var(--grid)}
  .add-row{border:1px solid var(--teal-header-dk);background:var(--teal-light);color:#08312c;font-family:inherit;font-weight:700;font-size:12px;padding:.3rem .75rem;border-radius:4px;cursor:pointer;display:inline-flex;align-items:center;gap:.35rem;margin-left:1.1rem}
  .add-row:hover{background:#d3f4f0}
  .add-row span{font-size:14px;line-height:1}

  /* read-only example */
  table.grid td.ex-a{background:var(--teal-light);color:#0a4a43;padding:.4rem .5rem;font-size:12px}
  table.grid td.ex-y{background:var(--yellow);padding:.4rem .5rem;font-size:12px}
  table.grid td.ex-ac{background:#fff;text-align:right;padding:.4rem .55rem;font-size:12px;font-variant-numeric:tabular-nums}
  table.grid tr.ex-total td{font-weight:700;font-size:12px}
  table.grid tr.ex-total .lbl{background:var(--teal-light);color:#08312c;padding:.4rem .5rem}
  table.grid tr.ex-total .dc{background:var(--yellow-bright);text-align:center;padding:.4rem .3rem}
  table.grid tr.ex-total .pink{background:var(--pink);text-align:right;padding:.4rem .55rem;font-variant-numeric:tabular-nums}
  table.grid tr.ex-total .teal{background:var(--teal-light)}
  .err{color:var(--red);font-weight:700}

  .toolbar{display:flex;gap:.5rem;margin-bottom:.7rem}
  .tool-btn{border:1px solid var(--grid);background:#fff;color:var(--ink-soft);font-family:inherit;font-size:11.5px;font-weight:600;padding:.32rem .7rem;border-radius:4px;cursor:pointer}
  .tool-btn:hover{background:var(--teal-light);color:#08312c;border-color:var(--teal-header-dk)}

  .submit-row{margin-top:1.6rem;display:flex;align-items:center;gap:1.2rem;flex-wrap:wrap;border-top:1px solid var(--grid-soft);padding-top:1.3rem}
  button.submit{font-family:inherit;font-weight:700;font-size:14px;background:var(--teal-header);color:#08312c;border:1px solid var(--teal-header-dk);padding:.7rem 1.8rem;border-radius:4px;cursor:pointer;transition:background .15s}
  button.submit:hover{background:var(--teal-header-dk);color:#fff}
  button.submit:disabled{opacity:.6;cursor:not-allowed}
  .count-note{font-size:12.5px;color:var(--ink-soft)}
  .count-note b{color:var(--ink);font-variant-numeric:tabular-nums}

  #status{margin-top:1rem;font-size:12.5px;padding:.7rem .9rem;border-radius:4px;display:none;white-space:pre-wrap}
  #status.show{display:block}
  #status.ok{background:var(--teal-light);border:1px solid var(--teal-header-dk);color:#08312c}
  #status.err{background:#fde9e9;border:1px solid #e0a0a0;color:#922}

  footer{text-align:center;color:var(--ink-soft);font-size:11px;margin-top:1.4rem;line-height:1.5}

  @media(max-width:920px){
    .layout{flex-direction:column;gap:.6rem}
    .cat-index{position:sticky;top:0;width:100%;max-height:none;border-radius:0;z-index:20}
    .ci-head{display:none}
    .ci-list{display:flex;overflow-x:auto;padding:.4rem .5rem;gap:.4rem}
    .ci-list a{flex:none;white-space:nowrap;border-left:none;border-bottom:3px solid transparent;border-radius:4px;padding:.35rem .6rem}
    .ci-list a.active{border-left:none;border-bottom-color:var(--teal-header)}
  }
  @media(max-width:700px){
    table.qa td.q{width:auto}
  }
</style>
</head>
<body>
<div class="layout">

  <nav class="cat-index" id="catIndex">
    <div class="ci-head">Categories</div>
    <ul class="ci-list" id="catList"></ul>
  </nav>

  <div class="sheet">
    <div class="sheet-tabs">
      <div class="tab" data-panel="panel-fund">1. Fund Details</div>
      <div class="tab" data-panel="panel-instructions">2. Instructions &amp; Example</div>
      <div class="tab active" data-panel="panel-screening">3. Master Screening File</div>
    </div>
    <div class="sheet-body">

      <!-- ===================== TAB 1: FUND DETAILS ===================== -->
      <section class="panel" id="panel-fund">
        <div class="action-note">ACTION: COMPLETE FOR NEW FUNDS</div>
        <div class="sheet-title">Fund Details</div>
        <table class="qa">
          <thead><tr><th>Question</th><th>Initial Response</th></tr></thead>
          <tbody>
            <tr><td class="q">Firm Name</td><td class="a"><input id="firmName" type="text"></td></tr>
            <tr><td class="q">Fund Name</td><td class="a"><input id="fundName" type="text" placeholder="Required"></td></tr>
            <tr><td class="q">Fund Identifier Code</td><td class="a"><input id="fundId" type="text" placeholder="e.g. ISIN / APIR"></td></tr>
            <tr><td class="q">Main Contact Name</td><td class="a"><input id="contactName" type="text"></td></tr>
            <tr><td class="q">Main Contact Email</td><td class="a"><input id="contactEmail" type="email"></td></tr>
            <tr><td class="q">Date of response</td><td class="a"><input id="dateResponse" type="date"></td></tr>
            <tr><td class="q">Date on which the data provided was last updated</td><td class="a"><input id="dateUpdated" type="date"></td></tr>
            <tr><td class="q">Do you apply screening approaches (positive or negative) as part of your investment process?</td>
                <td class="a"><select id="appliesScreening"><option value="">SELECT</option><option>Yes</option><option>No</option></select></td></tr>
            <tr><td class="q">How do you source screening data?</td>
                <td class="a"><select id="dataSource"><option value="">SELECT</option><option>Internal processes</option><option>External service providers</option><option>We do not collect screening data</option></select></td></tr>
            <tr><td class="q">Please provide the name of the external service provider(s) used to source screening data together with any relevant details regarding your processes. If not applicable please indicate N/A.</td>
                <td class="a"><textarea id="externalProvider" placeholder="N/A"></textarea></td></tr>
            <tr><td class="q">Do you have an exclusions list, document detailing your screening approach or similar in place? If so, please provide a link below (or note that you will email it).</td>
                <td class="a">
                  <select id="exclusionsList"><option value="">SELECT</option><option>Yes</option><option>No</option></select>
                  <input id="exclusionsDoc" class="qa-sub" type="text" placeholder="Link to document, or note you will email it">
                </td></tr>
            <tr><td class="q">General comments</td><td class="a"><textarea id="generalComments" placeholder="Any general comments or context for your responses…"></textarea></td></tr>
          </tbody>
        </table>
      </section>

      <!-- ===================== TAB 2: INSTRUCTIONS & EXAMPLE ===================== -->
      <section class="panel" id="panel-instructions">
        <div class="action-note info">ACTION: NONE — FOR INFORMATION</div>
        <div class="sheet-title">Instructions for completing screening</div>
        <ul class="instr-list">
          <li><b>a.</b> Where appropriate, we have referenced GICS® Sectors, Industry Groups, Industries and Sub-Industries (see <a href="https://www.msci.com/our-solutions/indexes/gics" target="_blank" rel="noopener">MSCI GICS</a>).</li>
          <li><b>b.</b> Using the <b>&ldquo;Data collection on category?&rdquo;</b> selector, indicate whether data is being collected on the category/industry, <b>regardless of holdings</b>. Setting it to <b>Yes</b> opens the activity so you can enter holdings.</li>
          <li><b>c.</b> Insofar as possible, data should be provided as at the earliest date possible.</li>
          <li><b>d.</b> When entering percentages, enter the numerical value only, rounded to two decimal places (e.g. <b>1.36</b> for 1.3623%).</li>
          <li><b>e.</b> Input data in the <b>yellow cells</b>: Holding, Portfolio Weight, Revenue Exposure, and Comments.</li>
          <li><b>f.</b> Screening can be based on many different considerations. To provide any general comments or details related to your responses, use the <b>1. Fund Details</b> tab — General comments.</li>
        </ul>

        <div class="ex-title">Example</div>
        <div class="table-scroll">
          <table class="grid">
            <thead><tr>
              <th>Activity</th><th>Data collection<br>on category?</th><th>Holding</th>
              <th>Portfolio Weight <span class="sub">%</span></th><th>Revenue Exposure <span class="sub">%</span></th>
              <th>Actual Exposure <span class="sub">%</span></th><th>Comments</th>
            </tr></thead>
            <tbody>
              <tr class="cat-band"><td colspan="7">ALCOHOL
A. Manufacture/production — revenue from manufacture/production of alcoholic beverage products (GICS Sub-industries: Brewers; Distillers &amp; Vintners)
B. Sale/supply — revenue from the sale/supply of alcoholic beverage products
C. Any tie — involvement in any related activity considered material to disclose</td></tr>

              <tr><td class="ex-a">Alcohol Manufacture/production</td><td class="ex-y"></td><td class="ex-y">N/A</td><td class="ex-ac">0.00</td><td class="ex-ac">0.00</td><td class="ex-ac">0.0000</td><td class="ex-y">N/A</td></tr>
              <tr><td class="ex-a">Alcohol Manufacture/production</td><td class="ex-y"></td><td class="ex-y">N/A</td><td class="ex-ac">0.00</td><td class="ex-ac">0.00</td><td class="ex-ac">0.0000</td><td class="ex-y">N/A</td></tr>
              <tr class="ex-total"><td class="teal"></td><td class="dc">No</td><td class="lbl">Total Alcohol Manufacture/production</td><td class="teal"></td><td class="teal"></td><td class="pink"></td><td class="teal">N/A</td></tr>

              <tr><td class="ex-a">Alcohol sale/supply</td><td class="ex-y"></td><td class="ex-y">WOW</td><td class="ex-ac">2.00</td><td class="ex-ac">1.50</td><td class="ex-ac">0.0300</td><td class="ex-y">1.5% of Woolworths revenue is derived from alcohol sales</td></tr>
              <tr><td class="ex-a">Alcohol sale/supply</td><td class="ex-y"></td><td class="ex-y">COL</td><td class="ex-ac">4.00</td><td class="ex-ac">9.00</td><td class="ex-ac">0.3600</td><td class="ex-y">9% of Coles revenue is derived from alcohol sales</td></tr>
              <tr class="ex-total"><td class="teal"></td><td class="dc">Yes</td><td class="lbl">Total Alcohol sale/supply</td><td class="teal"></td><td class="teal"></td><td class="pink">0.3900</td><td class="teal">N/A</td></tr>

              <tr><td class="ex-a">Alcohol Any tie</td><td class="ex-y"></td><td class="ex-y">ABC</td><td class="ex-ac">3.00</td><td class="ex-ac">10.00</td><td class="ex-ac">0.3000</td><td class="ex-y">N/A</td></tr>
              <tr><td class="ex-a">Alcohol Any tie</td><td class="ex-y"></td><td class="ex-y">DEF</td><td class="ex-ac">2.00</td><td class="ex-ac">1.00</td><td class="ex-ac">0.0200</td><td class="ex-y">N/A</td></tr>
              <tr><td class="ex-a">Alcohol Any tie</td><td class="ex-y"></td><td class="ex-y">XYZ</td><td class="ex-ac">5.00</td><td class="ex-ac">7.00</td><td class="ex-ac">0.3500</td><td class="ex-y">N/A</td></tr>
              <tr class="ex-total"><td class="teal"></td><td class="dc">SELECT</td><td class="lbl">Total Alcohol — Any tie</td><td class="teal"></td><td class="teal"></td><td class="pink err">ERROR</td><td class="teal">N/A</td></tr>
            </tbody>
          </table>
        </div>
        <div class="instruct" style="margin-top:1rem">
          <span>&#9432;</span>
          <div>In the example, the <b>SELECT / ERROR</b> on the last block shows what happens when &ldquo;Data collection on category?&rdquo; hasn&rsquo;t been answered &mdash; choose <b>Yes</b> or <b>No</b> to resolve it. <b>Actual Exposure = Portfolio Weight &times; Revenue Exposure &divide; 100</b>, and the <b>Total</b> sums the actual exposure for the activity.</div>
        </div>
      </section>

      <!-- ===================== TAB 3: MASTER SCREENING FILE ===================== -->
      <section class="panel active" id="panel-screening">
        <div class="action-note">ACTION: COMPLETE FOR NEW FUNDS</div>
        <div class="sheet-title">Master Screening File</div>

        <div class="instruct">
          <span>&#9432;</span>
          <div><b>Set &ldquo;Data collection on category?&rdquo; to Yes</b> to expand an activity and reveal its rows; <b>No</b> collapses it. <b>Input data in the yellow cells</b>, percentages as numeric values to two decimals (e.g. <b>1.36</b>). Each open activity shows five rows &mdash; use <b>Add row</b> for more. Fund identification is on the <b>1. Fund Details</b> tab.</div>
        </div>

        <div class="config-banner" id="configBanner">
          <span>&#9888;</span>
          <div><b>Setup required:</b> not connected to an inbox yet. Replace <code>YOUR_WEB3FORMS_ACCESS_KEY</code> in the script with your free key from web3forms.com.</div>
        </div>

        <div class="toolbar">
          <button class="tool-btn" id="expandAll" type="button">Expand all</button>
          <button class="tool-btn" id="collapseAll" type="button">Collapse all</button>
        </div>

        <div class="table-scroll">
          <table class="grid" id="screenTable">
            <thead><tr>
              <th>Activity</th><th>Data collection<br>on category?</th><th>Holding</th>
              <th>Portfolio Weight <span class="sub">%</span></th><th>Revenue Exposure <span class="sub">%</span></th>
              <th>Actual Exposure <span class="sub">%</span></th><th>Comments</th><th></th>
            </tr></thead>
          </table>
        </div>
      </section>

      <!-- common submit (applies to whole submission) -->
      <div class="submit-row">
        <button class="submit" id="submitBtn" type="button">Submit to screening inbox</button>
        <span class="count-note"><b id="filledCount">0</b> holding<span id="fcPlural">s</span> entered</span>
      </div>
      <div id="status"></div>

      <footer>Detailed Screening Template &middot; structured submission portal &middot; tabs mirror the workbook: Fund Details, Instructions &amp; Example, Master Screening File</footer>
    </div>
  </div>
</div>

<script>
/* ============================================================
   CONFIGURATION — EDIT THIS
   Get a free access key at https://web3forms.com (enter your inbox email there).
   ============================================================ */
const WEB3FORMS_ACCESS_KEY = "a24a57f4-8e46-4612-b1ed-2dc8681a503f";
/* ============================================================ */

const ROWS_PER_ACTIVITY = 5;

const CATALOGUE = {
  "Adult Entertainment / Pornography": ["Adult entertainment / pornography"],
  "Agricultural Assets": ["Agricultural assets"],
  "Alcohol": ["Alcohol — manufacture / production", "Alcohol — sale / supply", "Alcohol — any tie"],
  "Animal Cruelty": ["Animal cruelty"],
  "Armaments": ["Armaments — manufacture / production", "Armaments — sale"],
  "Fossil Fuels": ["Fossil fuels — oil sands", "Fossil fuels — oil & gas", "Fossil fuels — thermal coal", "Fossil fuels — any tie"],
  "Gambling": ["Gambling — ownership, operation & licencing", "Gambling — any tie"],
  "Gaming": ["Gaming"],
  "Modern Slavery Practices": ["Modern slavery practices"],
  "Payday Lending Practices": ["Payday lending practices"],
  "Predatory Lending Practices": ["Predatory lending practices"],
  "Prisons & Detention Centres": ["Prisons & detention centres"],
  "Tobacco": ["Tobacco — manufacture / production", "Tobacco — sale / supply", "Tobacco — any tie"],
  "Ultra-Processed Foods": ["Ultra-processed foods"],
  "Uranium Mining": ["Uranium mining"],
  "Water Assets": ["Water assets"]
};

const table = document.getElementById('screenTable');

/* ---------- tab switching ---------- */
function switchTab(panelId){
  document.querySelectorAll('.tab').forEach(t=> t.classList.toggle('active', t.dataset.panel===panelId));
  document.querySelectorAll('.panel').forEach(p=> p.classList.toggle('active', p.id===panelId));
  document.getElementById('catIndex').style.display = (panelId==='panel-screening') ? '' : 'none';
  window.scrollTo({top:0, behavior:'smooth'});
}
document.querySelectorAll('.tab').forEach(t=> t.addEventListener('click', ()=> switchTab(t.dataset.panel)));

/* ---------- screening table ---------- */
function dataRow(activity){
  const tr = document.createElement('tr');
  tr.className = 'data';
  tr.innerHTML = `
    <td class="activity-cell">${activity}</td>
    <td class="blankteal"></td>
    <td class="yellow holding"><input class="f-holding" type="text" placeholder="Name / ticker"></td>
    <td class="yellow num"><input class="f-weight" type="number" step="0.01" min="0" placeholder="0.00" inputmode="decimal"></td>
    <td class="yellow num"><input class="f-revenue" type="number" step="0.01" min="0" placeholder="0.00" inputmode="decimal"></td>
    <td class="actual"><span class="f-actual">0.0000</span></td>
    <td class="yellow comments"><input class="f-comments" type="text" placeholder="Optional comments"></td>
    <td class="rm"><button type="button" title="Remove row">&times;</button></td>`;
  const weight = tr.querySelector('.f-weight');
  const revenue = tr.querySelector('.f-revenue');
  const actual = tr.querySelector('.f-actual');
  const onInput = ()=>{
    const w = parseFloat(weight.value)||0, r = parseFloat(revenue.value)||0;
    actual.textContent = ((w*r)/100).toFixed(4);
    recalcGroup(tr.closest('tbody')); updateCount();
  };
  weight.addEventListener('input', onInput);
  revenue.addEventListener('input', onInput);
  tr.querySelector('.f-holding').addEventListener('input', updateCount);
  tr.querySelector('.rm button').addEventListener('click', ()=>{
    const body = tr.closest('tbody'); tr.remove(); recalcGroup(body); updateCount();
  });
  return tr;
}

function applyState(tb, focus){
  const sel = tb.querySelector('.f-dc');
  const open = sel.value === 'Yes';
  tb.classList.toggle('open', open);
  const lbl = tb.querySelector('.head-label .lbl');
  lbl.innerHTML = open ? ('Total ' + tb.dataset.activity)
                       : '<span class="hint">Set to &ldquo;Yes&rdquo; to enter holdings</span>';
  if(open && focus){ const f = tb.querySelector('tr.data .f-holding'); if(f) f.focus(); }
}

function buildGroup(activity){
  const tb = document.createElement('tbody');
  tb.className = 'group';
  tb.dataset.activity = activity;
  const head = document.createElement('tr');
  head.className = 'act-head';
  head.innerHTML = `
    <td class="toggle"><span class="chev">&#9654;</span> ${activity}</td>
    <td class="dc-cell"><select class="f-dc"><option value="">SELECT</option><option value="Yes">Yes</option><option value="No">No</option></select></td>
    <td class="head-label" colspan="3"><span class="lbl"></span></td>
    <td class="head-total"><span class="f-total">0.0000</span></td>
    <td class="head-end"></td>
    <td class="rm"></td>`;
  tb.appendChild(head);
  for(let i=0;i<ROWS_PER_ACTIVITY;i++) tb.appendChild(dataRow(activity));
  const adder = document.createElement('tr');
  adder.className = 'adder';
  adder.innerHTML = `<td></td><td></td><td colspan="6"><button class="add-row" type="button"><span>+</span> Add row</button></td>`;
  adder.querySelector('.add-row').addEventListener('click', ()=> tb.insertBefore(dataRow(activity), adder));
  tb.appendChild(adder);
  const sel = head.querySelector('.f-dc');
  sel.addEventListener('change', ()=> applyState(tb, true));
  head.querySelector('.toggle').addEventListener('click', ()=>{
    const open = tb.classList.contains('open');
    sel.value = open ? 'No' : 'Yes';
    applyState(tb, true);
  });
  applyState(tb, false);
  return tb;
}

function recalcGroup(tb){
  if(!tb) return;
  let sum = 0;
  tb.querySelectorAll('tr.data').forEach(r=> sum += parseFloat(r.querySelector('.f-actual').textContent)||0);
  const t = tb.querySelector('.f-total');
  if(t) t.textContent = sum.toFixed(4);
}

function buildSheet(){
  Object.entries(CATALOGUE).forEach(([cat, acts], idx)=>{
    const band = document.createElement('tbody');
    band.innerHTML = `<tr class="cat-band" id="cat-${idx}"><td colspan="8">${cat}</td></tr>`;
    table.appendChild(band);
    acts.forEach(a=> table.appendChild(buildGroup(a)));
  });
}

function buildIndex(){
  const ul = document.getElementById('catList');
  Object.keys(CATALOGUE).forEach((cat, idx)=>{
    const li = document.createElement('li');
    const a = document.createElement('a');
    a.href = '#cat-'+idx; a.textContent = cat; a.dataset.target = 'cat-'+idx;
    a.addEventListener('click', e=>{
      e.preventDefault();
      const el = document.getElementById('cat-'+idx);
      if(el) el.scrollIntoView({behavior:'smooth', block:'start'});
    });
    li.appendChild(a); ul.appendChild(li);
  });
}

function setupScrollSpy(){
  const links = [...document.querySelectorAll('#catList a')];
  const bands = [...document.querySelectorAll('tr.cat-band')];
  const isMobile = ()=> window.matchMedia('(max-width:920px)').matches;
  function update(){
    if(document.getElementById('catIndex').style.display==='none') return;
    const threshold = isMobile() ? 120 : 90;
    let activeId = bands.length ? bands[0].id : null;
    bands.forEach(b=>{ if(b.getBoundingClientRect().top - threshold <= 0) activeId = b.id; });
    links.forEach(a=>{
      const on = a.dataset.target === activeId;
      a.classList.toggle('active', on);
      if(on && isMobile()) a.scrollIntoView({inline:'center', block:'nearest'});
    });
  }
  let ticking = false;
  window.addEventListener('scroll', ()=>{ if(!ticking){ ticking=true; requestAnimationFrame(()=>{update(); ticking=false;}); } }, {passive:true});
  window.addEventListener('resize', update);
  update();
}

function setAll(open){
  table.querySelectorAll('tbody.group').forEach(tb=>{
    tb.querySelector('.f-dc').value = open ? 'Yes' : 'No';
    applyState(tb, false);
  });
}

function updateCount(){
  let n = 0;
  table.querySelectorAll('tr.data').forEach(r=>{ if(r.querySelector('.f-holding').value.trim()) n++; });
  document.getElementById('filledCount').textContent = n;
  document.getElementById('fcPlural').textContent = n===1?'':'s';
}

function val(id){ const el = document.getElementById(id); return el ? el.value.trim() : ''; }

function collect(){
  const activities = [];
  table.querySelectorAll('tbody.group').forEach(tb=>{
    const rows = [];
    tb.querySelectorAll('tr.data').forEach(r=>{
      const holding = r.querySelector('.f-holding').value.trim();
      if(!holding) return;
      const w = parseFloat(r.querySelector('.f-weight').value)||0;
      const rev = parseFloat(r.querySelector('.f-revenue').value)||0;
      rows.push({holding, portfolioWeight:w, revenueExposure:rev, actualExposure:+((w*rev)/100).toFixed(4), comments:r.querySelector('.f-comments').value.trim()});
    });
    const dc = tb.querySelector('.f-dc').value;
    if(rows.length || dc) activities.push({activity: tb.dataset.activity, dataCollection: dc, holdings: rows});
  });
  return {
    fundDetails: {
      firmName: val('firmName'), fundName: val('fundName'), fundId: val('fundId'),
      contactName: val('contactName'), contactEmail: val('contactEmail'),
      dateResponse: val('dateResponse'), dateUpdated: val('dateUpdated'),
      appliesScreening: val('appliesScreening'), dataSource: val('dataSource'),
      externalProvider: val('externalProvider'), exclusionsList: val('exclusionsList'),
      exclusionsDoc: val('exclusionsDoc'), generalComments: val('generalComments')
    },
    activities
  };
}

function buildSummary(d){
  const f = d.fundDetails;
  let t = `DETAILED SCREENING — SUBMISSION\n===============================\n\n`;
  t += `FUND DETAILS\n`;
  t += `Firm name: ${f.firmName||'(not provided)'}\n`;
  t += `Fund name: ${f.fundName||'(not provided)'}\n`;
  t += `Fund identifier code: ${f.fundId||'(not provided)'}\n`;
  t += `Main contact: ${f.contactName||'(not provided)'} <${f.contactEmail||'n/a'}>\n`;
  t += `Date of response: ${f.dateResponse||'(not provided)'}\n`;
  t += `Data last updated: ${f.dateUpdated||'(not provided)'}\n`;
  t += `Applies screening approaches: ${f.appliesScreening||'(blank)'}\n`;
  t += `Screening data source: ${f.dataSource||'(blank)'}\n`;
  t += `External provider(s): ${f.externalProvider||'(blank)'}\n`;
  t += `Exclusions list/document in place: ${f.exclusionsList||'(blank)'}`;
  t += f.exclusionsDoc ? `  (link/note: ${f.exclusionsDoc})\n` : `\n`;
  t += `General comments: ${f.generalComments||'(blank)'}\n`;
  t += `\nSCREENING\n`;
  d.activities.forEach(a=>{
    const tot = a.holdings.reduce((s,h)=>s+h.actualExposure,0).toFixed(4);
    t += `\n${a.activity}  [data collection: ${a.dataCollection||'(blank)'}]  — total actual exposure ${tot}%\n`;
    if(!a.holdings.length){ t += `   (no holdings entered)\n`; return; }
    a.holdings.forEach(h=>{
      t += `   • ${h.holding}: weight ${h.portfolioWeight}%, revenue ${h.revenueExposure}%, actual ${h.actualExposure}%`;
      t += h.comments ? `  — ${h.comments}\n` : `\n`;
    });
  });
  return t;
}

function validate(d){
  if(!d.fundDetails.fundName) return 'Please enter the Fund Name on the “1. Fund Details” tab.';
  if(!d.activities.some(a=>a.holdings.length>0)) return 'Please set an activity to “Yes” and enter at least one holding on the “3. Master Screening File” tab.';
  return null;
}

function showStatus(msg, ok){
  const s=document.getElementById('status');
  s.textContent=msg; s.className='show '+(ok?'ok':'err');
  s.scrollIntoView({behavior:'smooth',block:'center'});
}

document.getElementById('expandAll').addEventListener('click', ()=>setAll(true));
document.getElementById('collapseAll').addEventListener('click', ()=>setAll(false));

document.getElementById('submitBtn').addEventListener('click', async ()=>{
  const data = collect();
  const err = validate(data);
  if(err){
    // jump to the relevant tab to help the user
    if(err.includes('Fund Name')) switchTab('panel-fund'); else switchTab('panel-screening');
    showStatus(err,false); return;
  }
  const summary = buildSummary(data);
  const btn = document.getElementById('submitBtn');
  if(!WEB3FORMS_ACCESS_KEY || WEB3FORMS_ACCESS_KEY==="YOUR_WEB3FORMS_ACCESS_KEY"){
    showStatus("Not connected to an inbox yet — preview of what WOULD be sent:\n\n"+summary, false);
    return;
  }
  btn.disabled=true; btn.textContent='Sending…';
  try{
    const payload={access_key:WEB3FORMS_ACCESS_KEY,subject:`Screening submission — ${data.fundDetails.fundName}`,from_name:data.fundDetails.contactName||'Screening Portal',replyto:data.fundDetails.contactEmail||'',message:summary,data_json:JSON.stringify(data,null,2)};
    const res=await fetch('https://api.web3forms.com/submit',{method:'POST',headers:{'Content-Type':'application/json','Accept':'application/json'},body:JSON.stringify(payload)});
    const j=await res.json();
    if(j.success){ showStatus(`Submitted — screening for ${data.fundDetails.fundName} delivered to the inbox.`, true); }
    else{ showStatus('Delivery failed: '+(j.message||'unknown error')+'. Check the access key.', false); }
  }catch(ex){ showStatus('Network error: '+ex.message, false); }
  finally{ btn.disabled=false; btn.textContent='Submit to screening inbox'; }
});

/* init */
const today = new Date().toISOString().slice(0,10);
document.getElementById('dateResponse').value = today;
buildSheet();
buildIndex();
setupScrollSpy();
updateCount();
if(WEB3FORMS_ACCESS_KEY && WEB3FORMS_ACCESS_KEY!=="YOUR_WEB3FORMS_ACCESS_KEY"){
  document.getElementById('configBanner').style.display='none';
}
</script>
</body>
</html>
