```bash
git diff HEAD^ HEAD > diff_ultimo_commit.txt
```

{
"tarefa": "Realize uma auditoria completa do diff da branch atual em relação à branch de origem, verificando se a implementação atende integralmente aos requisitos da tarefa. A auditoria deve ser objetiva, rigorosa e baseada exclusivamente nas alterações apresentadas no diff e no contexto necessário para compreendê-las.",

"contexto": {
"descricao_tarefa": "[Descreva o que foi solicitado na tarefa.]",
"requisitos": [
"[Requisito obrigatório 1]",
"[Requisito obrigatório 2]",
"[Requisito obrigatório 3]"
],
"restricoes":
"[Restrição 1: o que não pode ser alterado.]",
"[Restrição 2: o que deve permanecer exatamente como está.]",
"[Restrição 3: alterações expressamente permitidas.]"
]
},

"diretrizes_auditoria": {
"D01": "Analise todas as alterações introduzidas pela branch, incluindo arquivos adicionados, removidos e modificados.",
"D02": "Verifique se cada requisito da tarefa foi efetivamente atendido, considerando a implementação apresentada no diff.",
"D03": "Verifique se as alterações respeitam todas as restrições estabelecidas para a tarefa.",
"D04": "Não considere uma implementação correta apenas porque o código compila, passa nos testes ou apresenta comportamento aparentemente equivalente. Verifique também o cumprimento dos requisitos estruturais e técnicos.",
"D05": "Não aceite alterações não autorizadas sob justificativas de melhoria de código, legibilidade, estilo, simplificação, correção de problemas preexistentes ou equivalência semântica.",
"D06": "Não proponha melhorias, refatorações ou alterações fora do escopo da tarefa.",
"D07": "Não presuma que uma alteração está correta sem evidências no código apresentado. Quando necessário, compare o código anterior e o código resultante.",
"D08": "Não investigue problemas preexistentes ou código não modificado, salvo quando forem indispensáveis para verificar um requisito diretamente relacionado às alterações da branch.",
"D09": "Diferencie violações comprovadas de situações que realmente não podem ser verificadas com as informações disponíveis. Não classifique como incerteza aquilo que não faz parte do escopo.",
"D10": "Considere os requisitos e as restrições como critérios obrigatórios de aprovação. Uma única violação comprovada é suficiente para reprovar a branch."
},

"criterio_aprovacao": "A branch somente poderá ser aprovada se todos os requisitos obrigatórios tiverem sido atendidos, todas as restrições tiverem sido respeitadas e nenhuma alteração não autorizada tiver sido identificada. Não utilize critérios subjetivos ou justificativas de equivalência para aprovar desvios.",

"saida": {
"status": "Responda APROVADO somente quando todos os critérios aplicáveis forem atendidos. Caso contrário, responda REPROVADO.",
"requisitos": "Apresente cada requisito e informe se foi ATENDIDO, NÃO ATENDIDO ou NÃO VERIFICÁVEL, acompanhado de evidências objetivas.",
"violacoes": "Para cada violação, informe o arquivo, o trecho ou função afetada, o requisito ou restrição descumprido e a justificativa técnica objetiva. Sempre que possível, apresente a diferença entre o código original e o código resultante.",
"incertezas": "Liste somente os pontos diretamente relacionados aos requisitos que realmente não puderam ser confirmados a partir das informações disponíveis. Explique o motivo.",
"resumo": "Apresente uma conclusão objetiva sobre a conformidade da branch."
}
}
IMPORTANTE: Não modifique o código, não aplique correções e não proponha soluções. Sua responsabilidade é exclusivamente auditar e emitir o resultado da validação.
