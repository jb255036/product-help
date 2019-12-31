<html><head></head><body><div class="nested0" aria-labelledby="ariaid-title1" topicindex="1" topicid="lyo1507821929412" id="lyo1507821929412"><h1 class="title topictitle1" id="ariaid-title1">LocalClusteringCoefficient (ML Engine)</h1><div class="body conbody">
<p class="p">The clustering coefficient, introduced by Watts and Strogatz in the
			context of binary undirected graphs, is frequently used for analyzing the structure of a
			network. The LocalClusteringCoefficient function extends the clustering coefficient to
			directed and weighted graphs. The LocalClusteringCoefficient function is based on the
			paper <cite class="cite">"Clustering in complex directed networks"</cite>by Georgio
			Fagiolo.</p>
<p class="p">For general information about the clustering coefficient, see <cite class="cite">D. J. Watts and S. H. Strogatz. Collective dynamics of "small-world"
				networks. Nature, 393:440–442, 1998</cite></p></div><div class="topic reference nested1" aria-labelledby="ariaid-title2" topicindex="2" topicid="jmz1507822498985" xml:lang="en-us" lang="en-us" id="jmz1507822498985">
<h2 class="title topictitle2" id="ariaid-title2">LocalClusteringCoefficient Syntax</h2><div class="body refbody"><div class="section" id="jmz1507822498985__section_N1000E_N1000C_N10001">
<h3 class="title sectiontitle">Version <span>1.3</span></h3><pre class="pre codeblock" xml:space="preserve"><code>SELECT * FROM LocalClusteringCoefficient (
  ON <var class="keyword varname">vertices_table</var> AS Vertices PARTITION BY <var class="keyword varname">vertex_key_column</var> [,...] 
  ON <var class="keyword varname">edges_table</var> AS Edges PARTITION BY <var class="keyword varname">source_vertex_key_column</var> [,...]
  USING
  TargetKey ({ '<var class="keyword varname">target_vertex_column</var>' | <var class="keyword varname">target_vertex_column_range</var> }[,...])
  [ Directed (<span><b>{'true'|'t'|'yes'|'y'|'1'|'false'|'f'|'no'|'n'|'0'}</b></span>) ]
  [ EdgeWeight ('<var class="keyword varname">edge_weight</var>') ]
  [ DegreeRange ({ '[<var class="keyword varname">min</var>:<var class="keyword varname">max</var>]' | '[<var class="keyword varname">min</var>:]' | '[:<var class="keyword varname">max</var>]' }) ]
  <code class="ph codeph">[ Accumulate ({ '<var class="keyword varname">accumulate_column</var>' | <var class="keyword varname">accumulate_column_range</var> }[,...]) ]</code>
) AS <var class="keyword varname">alias</var>;</code></pre>
<p class="p">In the DegreeRange syntax element, the brackets inside the single quotation marks are required. They do not indicate that their contents are optional.</p></div></div><div class="related-links"><div class="linklistheader"><p></p><b>Related Information</b></div>
<ul class="linklist linklist relinfo"><div class="linklistmember"><a href="ndv1557782188375.md">Column Specification Syntax Elements</a></div></ul></div></div><div class="topic reference nested1" aria-labelledby="ariaid-title3" topicindex="3" topicid="xos1507822657388" xml:lang="en-us" lang="en-us" id="xos1507822657388">
<h2 class="title topictitle2" id="ariaid-title3">LocalClusteringCoefficient Syntax Elements</h2><div class="body refbody"><div class="section" id="xos1507822657388__section_N10011_N1000E_N10001"><dl class="dl parml"><dt class="dt pt dlterm">TargetKey</dt><dd class="dd pd">Specify the key of the target vertex of an edge. The key consists of one or more Edges table column names.</dd><dt class="dt pt dlterm">Directed</dt><dd class="dd pd">[Optional] Specify whether the graph is directed.</dd><dd class="dd pd ddexpand">Default: 'false'</dd><dt class="dt pt dlterm">EdgeWeight</dt><dd class="dd pd">[Optional] Specify the name of the Edges table column that contains the edge weights. Each edge weight is a positive value in the range (0-1].</dd><dd class="dd pd ddexpand">Default behavior: The function treats the input graph as unweighted.</dd><dt class="dt pt dlterm">DegreeRange</dt><dd class="dd pd">[Optional] Specify the edge degree range—at least <var class="keyword varname">min</var> and at most <var class="keyword varname">max</var> (<code class="ph codeph">[<var class="keyword varname">min</var>:<var class="keyword varname">max</var>]</code>), at least <var class="keyword varname">min</var> (<code class="ph codeph">[<var class="keyword varname">min</var>:]</code>), or at most max (<code class="ph codeph">[:<var class="keyword varname">max</var>]</code>). The <var class="keyword varname">min</var> and <var class="keyword varname">max</var> must be positive integers. The function outputs only nodes with degrees in the specified range.</dd><dd class="dd pd ddexpand">Default behavior: The function outputs all nodes.</dd><dt class="dt pt dlterm">Accumulate</dt><dd class="dd pd">[Optional] Specify the names of the Vertices table columns to copy to the output table.</dd></dl></div></div></div></div></body></html>