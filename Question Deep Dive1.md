##### What is the result?
```Java
class One {
	static int x;
	int y;
	{x++; y++;} 
	static {x++;}
	One() {this(++x);}
	One(int x) {
		out.println(x + ", " + y);
	}
	static {new One();}
		public static void main(String[] args) {}
}
```

A) Compilation fails
B) Runs with no output
C) 2, 1
D) 3,1
E) 4,1

