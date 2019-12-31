<html><head></head><body><div class="nested0" aria-labelledby="ariaid-title1" topicindex="1" topicid="udx1507212896537" id="udx1507212896537"><h1 class="title topictitle1" id="ariaid-title1">LDA (ML Engine)</h1><div class="body conbody">
<p class="p">The LDA function uses training data and parameters to build a topic model, using an unsupervised method to estimate the correlation between the topics and words according to the topic number and other parameters. Optionally, the function creates the topic distributions for each training document.</p>
<p class="p">The function uses an iterative algorithm; therefore, applying it to large
			data sets with a large number of topics can be time-consuming.</p>
<p class="p">The function assumes that the model table can be fitted into the memory of
			the vworkers.</p></div><div class="topic reference nested1" aria-labelledby="ariaid-title2" topicindex="2" topicid="dil1507212961708" xml:lang="en-us" lang="en-us" id="dil1507212961708">
<h2 class="title topictitle2" id="ariaid-title2">LDA Syntax</h2><div class="body refbody"><div class="section" id="dil1507212961708__section_N1000E_N1000C_N10001">
<h3 class="title sectiontitle">Version 1.10</h3><pre class="pre codeblock" xml:space="preserve"><code>SELECT * FROM LDA (
  <span>ON { <var class="keyword varname">table</var> | <var class="keyword varname">view</var> | (<var class="keyword varname">query</var>) }</span> AS InputTable
  OUT TABLE ModelTable (<var class="keyword varname">model_table</var>)
  [ OUT TABLE OutputTable (<var class="keyword varname">output_table</var>) ]
  USING
  TopicNum ('<var class="keyword varname">topic_number</var>')
  [ Alpha (<var class="keyword varname">alpha</var>) ]
  [ Eta (<var class="keyword varname">eta</var>) ]
  DocIDColumn ('<var class="keyword varname">doc_id_column</var>')
  WordColumn ('<var class="keyword varname">word_column</var>')
  [ CountColumn ('<var class="keyword varname">count_column</var>') ]
  [ MaxIterNum (<var class="keyword varname">max_iterate</var>) ]
  [ StopThreshold (<var class="keyword varname">threshold</var>) ]
  [ Seed (<var class="keyword varname">seed</var>) ]
  [ OutputTopicNum ({ 'all' | <var class="keyword varname">num_topics</var> }) ]
  [ OutputTopicWordNum ({ 'none' | 'all' | '<var class="keyword varname">num_topic_words</var>' }) ]
  [ InitModelTaskCount (<var class="keyword varname">num_vworkers</var>) ]
) AS <var class="keyword varname">alias</var>;</code></pre></div></div></div><div class="topic reference nested1" aria-labelledby="ariaid-title3" topicindex="3" topicid="cgh1507213004499" xml:lang="en-us" lang="en-us" id="cgh1507213004499">
<h2 class="title topictitle2" id="ariaid-title3">LDA Syntax Elements</h2><div class="body refbody"><div class="section" id="cgh1507213004499__section_N10011_N1000E_N10001"><dl class="dl parml"><dt class="dt pt dlterm">ModelTable</dt><dd class="dd pd">Specify the name for the model table that the function creates in the database. This table must not already exist.</dd><dt class="dt pt dlterm">OutputTable</dt><dd class="dd pd">[Optional] Specify the name of the output table that contains the topic distribution of each document in the InputTable, which the function creates in the database. This table must not already exist. If you omit this syntax element, the function does not create this table.</dd><dt class="dt pt dlterm">TopicNum</dt><dd class="dd pd">Specify the number of topics for all the documents in the InputTable, an INTEGER value in the range [2, 1000].</dd><dt class="dt pt dlterm">Alpha</dt><dd class="dd pd">[Optional] Specify a hyperparameter of the model, the prior smooth parameter for the topic distribution over documents. As <var class="keyword varname">alpha</var> decreases, fewer topics are associated with each document.</dd><dd class="dd pd ddexpand">Default: 0.1</dd><dt class="dt pt dlterm">Eta</dt><dd class="dd pd">[Optional] Specify a hyperparameter of the model, the prior smooth parameter for the word distribution over topics. As <var class="keyword varname">eta</var> decreases, fewer words are associated with each topic.</dd><dd class="dd pd ddexpand">Default: 0.1</dd><dt class="dt pt dlterm">DocIDColumn</dt><dd class="dd pd">Specify the name of the input column that contains the document identifiers.</dd><dt class="dt pt dlterm">WordColumn</dt><dd class="dd pd">Specify the name of the InputTable column that contains the words (one word in each row).</dd><dt class="dt pt dlterm">CountColumn</dt><dd class="dd pd">[Optional] Specify the InputTable of the input column that contains the count of the corresponding word in the row, a positive value.</dd><dd class="dd pd ddexpand">Default behavior: The count of each word is 1.</dd><dt class="dt pt dlterm">MaxIterNum</dt><dd class="dd pd">[Optional] Specify the maximum number of iterations to perform if the model does not converge, a positive INTEGER value.</dd><dd class="dd pd ddexpand">Default: 50</dd><dt class="dt pt dlterm">StopThreshold</dt><dd class="dd pd">[Optional] Specify the convergence delta of log perplexity, a NUMERIC value in the range [0.0, 1.0].</dd><dd class="dd pd ddexpand">Default: 1e<span><sup>-4</sup></span></dd><dt class="dt pt dlterm">Seed</dt><dd class="dd pd">[Optional] Specify the random seed the algorithm uses for repeatable results. The <var class="keyword varname">seed</var> must be a LONG value.<div class="note note" id="cgh1507213004499__note_N100D0_N100C7_N100C0_N10018_N10014_N10010_N10001"><span><b>Note</b></span><div class="notebody"> For repeatable results, use both the Seed and UniqueID syntax elements. For more information, see <a href="qym1549987102806.md">Nondeterministic Results and UniqueID Syntax Element</a>.</div></div></dd><dt class="dt pt dlterm">OutputTopicNum</dt><dd class="dd pd">[Optional] Ignored unless OutputTable is specified. Specify the number of top-weighted topics to include, with their weights, in the output table for each training document:
<div class="tablenoborder"><table cellpadding="4" cellspacing="0" summary="" id="cgh1507213004499__table_jwz_tyy_fdb" class="table" frame="border" border="1" rules="all"><div class="caption"></div><colgroup span="1"><col style="width:50%" span="1"></col><col style="width:50%" span="1"></col></colgroup><thead class="thead" style="text-align:left;"><tr class="row"><th class="entry cellrowborder" style="vertical-align:top;" id="d46689e237" rowspan="1" colspan="1">Option</th><th class="entry cellrowborder" style="vertical-align:top;" id="d46689e239" rowspan="1" colspan="1">Description</th></tr></thead><tbody class="tbody"><tr class="row"><td class="entry cellrowborder" style="vertical-align:top;" headers="d46689e237" rowspan="1" colspan="1"><code class="ph codeph">'all'</code> (Default)</td><td class="entry cellrowborder" style="vertical-align:top;" headers="d46689e239" rowspan="1" colspan="1">All topics and their weights.</td></tr><tr class="row"><td class="entry cellrowborder" style="vertical-align:top;" headers="d46689e237" rowspan="1" colspan="1"><var class="keyword varname">num_topics</var></td><td class="entry cellrowborder" style="vertical-align:top;" headers="d46689e239" rowspan="1" colspan="1">Positive integer.</td></tr></tbody></table></div></dd><dt class="dt pt dlterm">OutputTopicWordNum</dt><dd class="dd pd">[Optional] Ignored unless OutputTable is specified. Specify the number of top topic words to include, with their topic identifiers, in the output table for each training document:
<div class="tablenoborder"><table cellpadding="4" cellspacing="0" summary="" id="cgh1507213004499__table_g3x_czy_fdb" class="table" frame="border" border="1" rules="all"><div class="caption"></div><colgroup span="1"><col style="width:50%" span="1"></col><col style="width:50%" span="1"></col></colgroup><thead class="thead" style="text-align:left;"><tr class="row"><th class="entry cellrowborder" style="vertical-align:top;" id="d46689e266" rowspan="1" colspan="1">Option</th><th class="entry cellrowborder" style="vertical-align:top;" id="d46689e268" rowspan="1" colspan="1">Description</th></tr></thead><tbody class="tbody"><tr class="row"><td class="entry cellrowborder" style="vertical-align:top;" headers="d46689e266" rowspan="1" colspan="1"><code class="ph codeph">'none'</code> (Default)</td><td class="entry cellrowborder" style="vertical-align:top;" headers="d46689e268" rowspan="1" colspan="1">No topic words or identifiers.</td></tr><tr class="row"><td class="entry cellrowborder" style="vertical-align:top;" headers="d46689e266" rowspan="1" colspan="1"><code class="ph codeph">'all'</code></td><td class="entry cellrowborder" style="vertical-align:top;" headers="d46689e268" rowspan="1" colspan="1">All topic words and their identifiers.</td></tr><tr class="row"><td class="entry cellrowborder" style="vertical-align:top;" headers="d46689e266" rowspan="1" colspan="1"><var class="keyword varname">num_topic_words</var></td><td class="entry cellrowborder" style="vertical-align:top;" headers="d46689e268" rowspan="1" colspan="1">Positive integer.</td></tr></tbody></table></div></dd><dt class="dt pt dlterm">InitModelTaskCount</dt><dd class="dd pd">[Optional] Specify the number of vworkers (an INTEGER value) to use to initialize the model. Use InitModelTaskCount with UniqueID to ensure the same results across cluster configurations.</dd><dd class="dd pd ddexpand">Default behavior: Function uses all available vworkers to initialize the model.</dd></dl><div class="note note" id="cgh1507213004499__note_N10129_N10126_N1000C_N10001"><span><b>Note</b></span><div class="notebody">Seed settings and cluster configurations affect function results.</div></div></div></div></div></div></body></html>