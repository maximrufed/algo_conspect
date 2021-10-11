## B - дерево

- Каждая вершина содержит k(v) ключей x0 < x1 < ... < x_(v(k) - 1)  
Указатели на поддеревья (их будет k(v) + 1) a0, a1, a2 ... a_k(v)  
В a_0 все ключи меньше x0  
В a_k(v) ключи больше x_v(k) - 1  
В a_i все ключи больше x_(i - 1) и меньше x_(i)  
- Зафиксироавна констатна t >= 2 : 
	- В любой вершине v : k(v) <= 2 * t - 1
	- В любой некорневой вершине : k(v) >= t - 1
- Все пустые вершины находятся на одной и той-же глубине

Например, при t = 3, k(v) = [2 .. 5]
// TODO Picture

h - высота дерева  
n - количество влючей  
n >= 1 + 2(t - 1) + 2 (t - 1) * t + 2(t - 1) * t^2 + 2(t - 1) * t^3 + ... + 2(t - 1) * t^(h - 1)  
= 1 + 2(t - 1) * (t^h - 1) / (t - 1) = 2 * t^h - 1  
h <= log(t, (n + 1) / 2) (t - основание  

	struct Node {
		vector<T> keys;
		vector<NodeID> children;
	}

Мы пытаемся уменьшить количество обращений к памяти, поэтому жертвуем временем.  

#### search

	bool search(T key, NodeID root) {
		Node v = ReadFromDisk(root);
		while (true) {
			int ind = std::lower_bound(v.keys.begin(), v.keys.end(), key);
			if (ind != v.keys.end() && *ind == key) return true;
			NodeID child = v.children[ind - v.keys.begin()]
			if (!is_valid(child)) {
				// Это лист
				return false;
			}
			v = ReadFromDisk(child);
		}
	}


