**RBAC (Role-Based Access Control):** Controle de acesso baseado em papéis (ex.: `Admin`, `Developer`, `Member`). As permissões são agrupadas em roles e atribuídas aos usuários inclusive quando o sistema permite criar roles personalizadas marcando permissões em uma grade.

**ABAC (Attribute-Based Access Control):** Controle de acesso dinâmico baseado na avaliação de atributos do usuário, do recurso, da ação e do contexto (ex.: permitir edição apenas se o usuário for o dono do registro e o status estiver como rascunho).

**Modelo Híbrido (RBAC + ABAC):** Sistemas flexíveis combinam os dois modelos: usam **RBAC** para definir o que o papel pode fazer no sistema e **ABAC** para filtrar sobre quais dados e em quais condições essa ação é permitida.