Labeled LDA [[Ramage+EMNLP2009]Labeled LDA: A supervised topic model for credit attribution in multi-labeled corpora]()

[python implementation](http://shuyo.wordpress.com/2013/07/24/python-implementation-of-labeled-lda-ramage-emnlp2009/)

pros: easy to implement
cons: It is necessary to specify label-topic correspondence manually. DP-MRM [[Kim+ICML2012]Dirichlet Process with Mixed Random Measures: A Nonparametric Topic Model for Labeled Data]()

Bernoulli distribution: 

$$f(k;p)=\begin{ cases } p\quad \quad \quad if\quad k=1 \\ 1-p\quad if\quad k=0 \end{ cases }$$

Gamma function:

$$\Gamma \left( x \right) =\int _{ 0 }^{ \infty  }{ { t }^{ x-1 }{ e }^{ -t }dt } $$ 
$$\Gamma \left( x+1 \right) =x\Gamma \left( x \right) $$
$$\Gamma \left( n \right) =\left( n-1 \right) !$$

Beta function: 

$$B\left( m,n \right) =\int _{ 0 }^{ 1 }{ { x }^{ m-1 }{ \left( 1-x \right)  }^{ n-1 }dx } $$
$$B\left( m,n \right) =\frac { \Gamma \left( m \right) \Gamma \left( n \right)  }{ \Gamma \left( m+n \right)  } $$


	