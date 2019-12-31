<html><head></head><body><div class="nested0" aria-labelledby="ariaid-title1" topicindex="1" topicid="zwu1507904746201" id="zwu1507904746201"><h1 class="title topictitle1" id="ariaid-title1">FellegiSunter (ML Engine)</h1><div class="body conbody">
<p class="p">The FellegiSunter function estimates the parameters of the Fellegi-Sunter model.</p>
<p class="p">The function can use either supervised or unsupervised learning. For supervised learning, specify the TagColumn syntax element. For unsupervised learning, omit the TagColumn syntax element and specify the syntax elements InitialM, InitialU, InitialP, and MaxIteration.</p></div><div class="topic reference nested1" aria-labelledby="ariaid-title2" topicindex="2" topicid="avv1507904892163" xml:lang="en-us" lang="en-us" id="avv1507904892163">
<h2 class="title topictitle2" id="ariaid-title2">FellegiSunter Syntax</h2><div class="body refbody"><div class="section" id="avv1507904892163__section_N1000E_N1000C_N10001">
<h3 class="title sectiontitle">Version <span>1.7</span></h3><pre class="pre codeblock" xml:space="preserve"><code>SELECT * FROM FellegiSunter (
  <span>ON { <var class="keyword varname">table</var> | <var class="keyword varname">view</var> | (<var class="keyword varname">query</var>) }</span> AS InputTable
  USING
  ComparisonFields ('<var class="keyword varname">field</var>[:<var class="keyword varname">threshold_value</var>]' [,...])
  [ TagColumn ('<var class="keyword varname">tag_column</var>') ]
  [ InitialM (<var class="keyword varname">initial_value_of_M</var>) ]
  [ InitialU (<var class="keyword varname">initial_value_of_U</var>) ]
  [ InitialP (<var class="keyword varname">initial_value_of_P</var>) ]
  [ MaxIterNum (<var class="keyword varname">max_iteration_number</var>) ]
  [ Eta (<var class="keyword varname">eta_value</var>) ]
  [ Lambda (<var class="keyword varname">lambda_value</var>) ]
  [ Mu (<var class="keyword varname">mu_value</var>) ]
) AS <var class="keyword varname">alias</var>;</code></pre></div></div></div><div class="topic reference nested1" aria-labelledby="ariaid-title3" topicindex="3" topicid="qgw1507904896522" xml:lang="en-us" lang="en-us" id="qgw1507904896522">
<h2 class="title topictitle2" id="ariaid-title3">FellegiSunter Syntax Elements</h2><div class="body refbody"><div class="section" id="qgw1507904896522__section_N10011_N1000E_N10001"><dl class="dl parml"><dt class="dt pt dlterm">ComparisonFields</dt><dd class="dd pd">Specify the columns of InputTable to use in the field-pair similarity in the training process. If the value in the column is less than <var class="keyword varname">threshold_value</var>, the field pair does not agree; otherwise, the field pair agrees.</dd><dd class="dd pd ddexpand">Default behavior: The <var class="keyword varname">threshold_value</var> of each field is 1.</dd><dt class="dt pt dlterm">TagColumn</dt><dd class="dd pd">[Optional] If you specify this syntax element, the function uses supervised learning; if you omit it, the function uses unsupervised learning.
<p class="p">This syntax element specifies the name of the column that indicates whether two objects match. The column must contain only the values 'M' (matched) and 'U' (unmatched).</p></dd><dt class="dt pt dlterm">InitialM</dt><dd class="dd pd">[Optional] For unsupervised learning, this syntax element specifies the initial value of m, which is the probability that a field agrees, given that the object-pair belongs to the same object. For supervised learning, the function ignores this syntax element.</dd><dd class="dd pd ddexpand">Default: 0.9</dd><dt class="dt pt dlterm">InitialU</dt><dd class="dd pd">[Optional] For unsupervised learning, this syntax element specifies the initial value of u, which is the probability that a field agrees, given that the object-pair belongs to a different object. For supervised learning, the function ignores this syntax element.</dd><dd class="dd pd ddexpand">Default: 0.1</dd><dt class="dt pt dlterm">InitialP</dt><dd class="dd pd">[Optional] </dd><dd class="dd pd ddexpand">For unsupervised learning, this syntax element specifies the initial value of p, which is the percentage of all possible object-pairs that contain the same object. For supervised learning, the function ignores this syntax element.</dd><dd class="dd pd ddexpand">Default: 0.1</dd><dt class="dt pt dlterm">MaxIterNum</dt><dd class="dd pd">[Optional] For unsupervised learning, this syntax element specifies the maximum number of iterations. For supervised learning, the function ignores this syntax element.</dd><dd class="dd pd ddexpand">Default: 100</dd><dt class="dt pt dlterm">Eta</dt><dd class="dd pd">[Optional] For unsupervised learning, this syntax element specifies the tolerance of the termination criterion. At the end of each iteration, the function computes the difference between the current value of p and the value of p at the end of the previous iteration. If the difference is less than <var class="keyword varname">eta_value</var>, the function terminates.</dd><dd class="dd pd ddexpand">Default: 1*10<span><sup>-5</sup></span></dd><dt class="dt pt dlterm">Lambda</dt><dd class="dd pd">[Optional] </dd><dd class="dd pd ddexpand">Specify the Type I (false negative) error, which occurs if an unmatched comparison is erroneously linked.</dd><dd class="dd pd ddexpand">Default: 0.9</dd><dt class="dt pt dlterm">Mu</dt><dd class="dd pd">[Optional] Specify the Type II (false positive) error, which occurs if a matched comparison is erroneously not linked.</dd><dd class="dd pd ddexpand">Default: 0.9</dd></dl><div class="note note" id="qgw1507904896522__note_N100E0_N100DD_N1000C_N10001"><span><b>Note</b></span><div class="notebody">Lambda and Mu determine the values of the model properties <var class="keyword varname">lower_bound</var> and <var class="keyword varname">upper_bound</var>. For details, see: <cite class="cite">Fellegi, Ivan; Sunter, Alan (December 1969). "A Theory for Record Linkage" Journal of the American Statistical Association 64</cite></div></div></div></div></div></div></body></html>