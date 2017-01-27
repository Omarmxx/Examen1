
package examen;


public class Edge {
Object Element;
	boolean directed;
	Vertex v1;
	Vertex v2;
	int pos;
	static int cv=0;
	/** Creates a new instance of Edge */
	public Edge() {
		cv++;
	}
	public Edge(Vertex v,Vertex w,Object O) {
		cv++;
		v1=v;
		v2=w;
		Element=O;
		directed=false;
	}
	public Vertex getV1()
	{
		return v1;
	}
	public Vertex getV2()
	{ 
		return v2;
	}
}
package examen;
import java.util.*;
public interface Graph {
  
	//Regresa la cantidad de vértices en G
	public int numVertices();
	//Regresa la cantidad de aristas en G
	public int numEdges();
	//Regresa una lista de los vértices de G
	public LinkedList vertices();
	//Regresa una lista de las aristas de G
	public LinkedList edges();
	//Regresa el grado de V
	public int degree(Vertex V);
	public int degreeInput(Vertex V);
	public int degreeOutput(Vertex V);
	//Regresa un iterador de los vértices adyacentes a V
	public LinkedList adjacentVertices(Vertex V);
	//Regresa un iterador de las aristas que inciden en V
	public LinkedList incidentEdges(Vertex V);
	//Inserta una nueva arista
	public Edge insertEdge(Vertex v, Vertex w,Object O,boolean d);
	//Inserta y regresa un nuevo vértice
	public Vertex insertVertex(Object O);
	//public Vertice search(int x);
	public String dfs();


package examen;
import java.util.*;
public class ListEdgesGraph implements Graph {
public LinkedList lv=new LinkedList();
	public LinkedList le=new LinkedList();
	//Contadores para adicionar elementos en las listas
	int cv=0;
	int ce=0;
	public ListEdgesGraph()
	{
	}
	public int numVertices()
	{
		return lv.size();
	}
	//Regresa la cantidad de aristas en G

	public int numEdges()
	{
		return le.size();
	}
	//Regresa una lista con los vértices de G
	public LinkedList vertices()
	{
		return lv;
	}
	//Regresa una lista con las aristas de G
	public LinkedList edges()
	{
		return le;
	}
	//Inserta y regresa un nuevo vértice
	public Vertex insertVertex(Object O)
	{
		Vertex v=new Vertex(O);
		lv.add(cv++,v);
		return v;
	}
	//Inserta y regresa una nueva arista
	public Edge insertEdge(Vertex v, Vertex w,Object O,boolean d)
	{
		int x,y;
		Edge e=new Edge(v,w,O);
		le.add(ce++,e);
		if (d==true)
		{
			System.out.println("Entre por true");
			x=v.getEo();//LAS QUE SALEN
			x++;
			v.setEo(x);
			y=w.getEin();//LAS QUE ENTRAN
			y++;
			w.setEin(y);//profe tenia un error tenia v, en vez de w
		}
		else
		{
			x=v.getEi();
			x++;
			v.setEi(x);
			y=w.getEi();
			y++;
			w.setEi(y);
		}
		return e;
	}
	//Regresa el grado de V
	public int degree(Vertex V)
	{
		for (int i=0;i<lv.size(); i++)
		{
			Vertex V2=(Vertex)lv.get(i);
			if (V==V2)
			{
				return V.getEi();
			}
		}
		return 0;
		
	}
	//Regresa el numero de aristas que entran a V
	public int degreeInput(Vertex V)
	{
		return V.getEin();	
	}
	//regresa el numero de Aristas que salen de V
	public int degreeOutput(Vertex V)
	{
		return V.getEo();	
	}
	//Regresa una lista de los vértices adyacentes a V
	public LinkedList adjacentVertices(Vertex V)
	{
		LinkedList L=new LinkedList();
		int c=0;
		for (int i=0;i<le.size(); i++)
		{ 
			Edge e=(Edge)le.get(i);
			Vertex V1=e.getV1();
			Vertex V2=e.getV2();
			if (V1==V)
			{
				L.add (c++,V2);
			}
			if (V2==V)
			{
				L.add (c++,V1);
			}
		}
		return L;
	}
	//Regresa un iterador de las aristas que inciden en V
	public LinkedList incidentEdges(Vertex V)
	{
		LinkedList L=new LinkedList();
		int c=0;
		for (int i=0;i<le.size(); i++)
		{ 
			Edge e=(Edge)le.get(i);
			Vertex V1=e.getV1();
			Vertex V2=e.getV2();
			if (V1==V)
			{ 
				L.add (c++,e);
			}
			if (V2==V)
			{ 
				L.add (c++,e);
			}
		}
		return L;
	}
	//Regresa el recorrido dfs de G
	public String dfs()
	{
		for (int i=0;i<lv.size(); i++)
		{ 
			Vertex w=(Vertex)lv.get(i);
			w.setState(0);
		}
		LinkedList L=new LinkedList();
		LinkedList L2=new LinkedList();
		int c=0;
		Vertex w=(Vertex)lv.get(0);
		L.add(c++,w);
		w.setState(1);
		String r="";
		while (L.size() !=0)
		{
			w=(Vertex)L.getFirst();
			//System.out.println(w.getElement());
			r=r+w.getElement();
			w.setState(3);
			c--;
			L.removeFirst();
			L2=adjacentVertices(w);
			for (int i=0;i<L2.size(); i++)
			{ 
				Vertex y=(Vertex)L2.get(i);
				if (y.getState()==0) 
				{
					L.add(c++,y);
					y.setState(2);
				}
			}
		}
	return r;
	}

    Vertex insertVertex(String a) {
        throw new UnsupportedOperationException("Not supported yet."); 
    }
}
package examen;

public class Vertex {
Object element;
	private int ei;//CUANDO EL GRAFO ES NO DIRIGIDO
	private int eo;//Cuando el grafo es dirigido
	private int ein;//cuando el grafo es dirigido
	int pos;
	private int state;
	static int ce=0;
	/** Creates a new instance of Vertex */
	public Vertex() {
		ei=0;
		eo=0;
		ein=0;
		element=null;
		pos=ce++;
	}
	public Vertex(Object O) {
		element=O;
		pos=ce++;
	}
	public void setElement(Object O)
	{
	
	}
	public Object getElement()
	{
		return element;
	}
	public int getEi()
	{
		return ei;
	}
	public int getEo()
	{
		return eo;
	}
	public int getEin()
	{
		return ein;
	}
	public void setEi(int x)
	{
		ei=x;
	}
	public void setEo(int x)
	{
		eo=x;
	}
	public void setEin(int x)
	{
		ein=x;
	}
	public void setState(int x)
	{
		state=x;
	}
	public int getState(){
            return state;
        }
}




package examen;
import java.lang.*;
import java.io.*;
import java.util.*;
	public class Main
	{
		public Main() 
		{
		}
		public static void main(String[] args) 
		{
		// TODO code application logic here
			String r="";
			ListEdgesGraph g=new ListEdgesGraph();
			Vertex v1=g.insertVertex("A");
			Vertex v2=g.insertVertex("B");
			g.insertEdge(v1,v2,1,false);
			Vertex v3=g.insertVertex("C");
			g.insertEdge(v2,v3,1,false);
			Vertex v4=g.insertVertex("D");
			g.insertEdge(v3,v4,1,false);
			Vertex v5=g.insertVertex("E");
			g.insertEdge(v1,v5,1,false);
			g.insertEdge(v2,v5,1,false);
			g.insertEdge(v3,v5,1,false);
			Vertex v6=g.insertVertex("F");
			g.insertEdge(v3,v6,1,false);
			Vertex v7=g.insertVertex("G");
			g.insertEdge(v5,v7,1,false);
			Vertex v8=g.insertVertex("H");
			g.insertEdge(v1,v8,1,false);
			g.insertEdge(v5,v8,1,false);
			Vertex v9=g.insertVertex("I");
			g.insertEdge(v8,v9,1,false);
			Vertex v10=g.insertVertex("J");
			g.insertEdge(v6,v10,1,false);
			g.insertEdge(v8,v10,1,false);
			g.insertEdge(v7,v10,1,false);
			System.out.println("Numero de vertices: "+g.numVertices());
			System.out.println("Numero de aristas: "+g.numEdges());
			System.out.println("Grado del vertice A: "+g.degree(v1));
			System.out.println("Grado del vertice H: "+g.degree(v8));
			r=g.dfs();
			System.out.println("Recorrido bfs del grafo "+r);
			
			System.out.println("Este codigo lo agrege yo");
			Vertex v11=g.insertVertex("K");
			Vertex v12=g.insertVertex("L");
			Vertex v13=g.insertVertex("M");
			Vertex v14=g.insertVertex("N");
			//salen de m
			g.insertEdge(v11,v12,1,true);
			g.insertEdge(v11,v13,1,true);
			g.insertEdge(v11,v14,1,true);
			//salen de l
			g.insertEdge(v12,v11,1,true);
			//SALEN DE M
			g.insertEdge(v13,v12,1,true);
			//salen de n
			g.insertEdge(v14,v13,1,true);
			System.out.println("Aristas que entran a K " + g.degreeInput(v11));
			System.out.println("Aristas que entran a L " + g.degreeInput(v12));
			System.out.println("Aristas que entran a M " + g.degreeInput(v13));
			System.out.println("Aristas que entran a N " + g.degreeInput(v14));
			System.out.println("Aristas que salen de K " + g.degreeOutput(v11));
			System.out.println("Aristas que salen de L " + g.degreeOutput(v12));
			System.out.println("Aristas que salen de M " + g.degreeOutput(v13));
			System.out.println("Aristas que salen de N " + g.degreeOutput(v14));
		}
}
