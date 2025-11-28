# Evidencia de Problemas de Programación
### Luis Fernando Martinez Barragan - A01613426

## Problemas Resueltos

### 2164. Sort Even and Odd Indices Independently
**Problema:** [LeetCode 2164](https://leetcode.com/problems/sort-even-and-odd-indices-independently/description/)  
**Video Explicativo:** [Ver en Drive](https://drive.google.com/file/d/1CW3bYLzwwkn2FVeRaHJyuqoR-1Q2sfui/view?usp=sharing)  
**Solucion:** [Ver Solución](https://leetcode.com/problems/sort-even-and-odd-indices-independently/solutions/7379440/ordenacion-por-separado-by-luisfer006-as6f)

**Estrategia:**

Separar los valores del arreglo en dos listas, una para  pares y otro para impares, esto con el fin de simplificar

Ordenar la lista de pares en orden ascendente y la de impares en orden descendente, justo como lo solicita el problema 

Reconstruir el arreglo original ordenando en cada posición el siguiente valor de la lista, usando pares para la posicion de los pares e impares en la posicion de los impares


**Codigo** 
```
cpp
/*
   Author: Luis Fernando Martinez Barragan - A01613426
   Date: 04 - 11 - 2025
   Problema 1
*/
class Solution {
public:
    vector<int> sortEvenOdd(vector<int>& nums) {
        vector<int> pares, impares;

        for (int i = 0; i < nums.size(); i++) {
            if (i % 2 == 0) pares.push_back(nums[i]);
            else impares.push_back(nums[i]);
        }

        sort(pares.begin(), pares.end());
        sort(impares.begin(), impares.end(), greater<int>());

        int p = 0, im = 0;

        for (int i = 0; i < nums.size(); i++) {
            if (i % 2 == 0) nums[i] = pares[p++];
            else nums[i] = impares[im++];
        }

        return nums;
    }
};
```

### 203. Remove Linked List Elements

**Problema:** [LeetCode 2164](https://leetcode.com/problems/remove-linked-list-elements/description/)  
**Video Explicativo:** [Ver en Drive](https://drive.google.com/file/d/1bOYX_HWZW-iQ8wF9q5ctSFekFzT6IVAu/view?usp=sharing)  
**Solucion:** [Ver Solución](https://leetcode.com/problems/remove-linked-list-elements/solutions/7379472/eliminacion-de-nodos-con-valor-especific-6dp5)

**Estrategia:**

Necesitaba una forma segura de borrar el primer nodo, asi que agregue un nodo extra al inicio para no tener ningun problema

Quiero revisar cada nodo sin eliminar nada de la estructura, por eso analizamos actual->next en vez de moverme de golpe

Cuando encuentro el valor que quiero eliminar simplemente salto ese nodo, así mantengo la lista limpia sin necesidad de borrar memoria manualmente dentro del ciclo

```
cpp
/*
   Author: Luis Fernando Martinez Barragan - A01613426
   Date: 16 - 11 - 2025
   Problema 1
*/
class Solution {
public:
    ListNode* removeElements(ListNode* cabeza, int valorBorrar) {
        ListNode* nr = new ListNode(0);
        nr->next = cabeza;

        ListNode* actual = nr;

        while (actual->next != nullptr) {
            if (actual->next->val == valorBorrar) {
                actual->next = actual->next->next;
            } else {
                actual = actual->next;
            }
        }

        ListNode* nuevaCabeza = nr->next;
        delete nr;
        return nuevaCabeza;
    }
};
```

### 173. Binary Search Tree Iterator
**Problema:** [LeetCode 2164](https://leetcode.com/problems/binary-search-tree-iterator/description/)  
**Video Explicativo:** [Ver en Drive](https://drive.google.com/file/d/1MSRsMhcMhAgh9irfbmnmmnzvkG5kl1ic/view?usp=sharing)  
**Solucion:** [Ver Solución](https://leetcode.com/problems/binary-search-tree-iterator/solutions/7379505/iterador-de-bst-by-luisfer006-gfco)

**Estrategia:**

Decidi recorrer todo el arbol en in-order desde el constructor para obtener los numeros ya ordenados

Guarde esos valores en un vector, porque asi es mucho mas facil iterar sin necesidad de punteros o asi

Use un indice para avanzar, dejando que next() y hasNext() sean operaciones simples

```
cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */

/*
   Author: Luis Fernando Martinez Barragan - A01613426
   Date: 26 - 11 - 2025
   Problema 1
*/
class BSTIterator {
public:
    vector<int> valores;  
    int indice;

    BSTIterator(TreeNode* root) {
        recorrerInorder(root);
        indice = 0;
    }
    
    void recorrerInorder(TreeNode* nodo) {
        if (nodo == nullptr) return;
        recorrerInorder(nodo->left);
        valores.push_back(nodo->val);
        recorrerInorder(nodo->right);
    }

    int next() {
        return valores[indice++];
    }
    
    bool hasNext() {
        return indice < valores.size();
    }
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator* obj = new BSTIterator(root);
 * int param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```
