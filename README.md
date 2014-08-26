stuff
=====
XML uitlezen
=====
	/*Document doc = readDocument("plattegrond.xml");
		XPath xp = XPathFactory.newInstance().newXPath();
		String queryVan = "/plattegrond/wegen/van";
		Graph<String> graph = new Graph<String>();
		if (doc != null) {
			 System.out.println("Succes");
			try {
				NodeList nodelist = (NodeList) xp.compile(queryVan).evaluate(doc,
						XPathConstants.NODESET);
				for (int i = 0; i < nodelist.getLength(); i++) {
					Node node = nodelist.item(i);
					Element e = (Element) node;
					
					String van = e.getElementsByTagName("plaats").item(0).getTextContent();
					
					if (!graph.hasVertex(van)) {
						graph.putVertex(van);
					}
					if (e.getElementsByTagName("naar").getLength() > 0) {
						NodeList n = e.getElementsByTagName("plaats");
							//door de "1" ipv "0" pakt hij niet de eerste plaats die bedoelt is voor "van" maar alle andere die boelt zijn voor "naar"
							for (int j = 1; j < n.getLength(); j++) {
								Element el = (Element) n.item(j);
								String naar = el.getTextContent();
								
								if (!graph.hasVertex(naar))
								{
									graph.putVertex(naar);
								}
								
								if (!graph.hasEdge(van, naar)) {
									graph.putEdge(van, naar);
								}
							}
						}
					

				}

			} catch (XPathExpressionException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			System.out.println(graph.toString());

		} else {
			System.out.println("Document not found");
		}*/
		
====
Depth First Search
====
	/*public static void DPS(String zoek, String currentNode,
			Set<String> visited, Graph<String> graph) {
			visited.add(currentNode);

			System.out.println(currentNode);

			if (currentNode.equals(zoek)) {
				System.out.println("Done");
				return;
			} else {
				for (String neighbour : graph.neighbours(currentNode)) {
					if (!visited.contains(neighbour)) {
						DPS(zoek, neighbour, visited, graph);
					}
				}
			}*/
====
Breadth First Search
====
	public void bfs()
	{
		// BFS uses Queue data structure
		Queue queue = new LinkedList();
		queue.add(this.rootNode);
		printNode(this.rootNode);
		rootNode.visited = true;
		while(!queue.isEmpty()) {
			Node node = (Node)queue.remove();
			Node child=null;
			while((child=getUnvisitedChildNode(node))!=null) {
				child.visited=true;
				printNode(child);
				queue.add(child);
			}
		}
		// Clear visited property of nodes
		clearNodes();
	}
====
Tree
====
	public int nrOfLeaves()
	{
		if( isEmpty() )
		    return 0;
		  if( left == null && right == null ) {
		    return 1;
		  } else {
		    return left.nrOfLeaves() + right.nrOfLeaves();
		  }
	}
	public void pruneRight()
	{
		if(right.isEmpty())
		{
			return;
		}
		else if(left.isEmpty()){
			return;
		}
		else{
			right = new AssessmentTree<K,V>();
			left.pruneRight();
		}
	}
