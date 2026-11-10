# mdm-pkg-store
Loja Oficial de futebol para Ps4.
<!doctype html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="theme-color" content="#090b12">
<title>MDM PKG Store</title>
<style>
:root{color-scheme:dark;--bg:#090b12;--panel:#151a29;--line:#2a3044;--text:#f4f5ff;--muted:#aab2c8;--accent:#8b5cf6;--blue:#536dfe}
*{box-sizing:border-box}body{margin:0;background:radial-gradient(ellipse at top,#201747 0,#090b12 52%);color:var(--text);font:16px/1.5 system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif}
header{padding:26px 18px 22px;border-bottom:1px solid var(--line);background:#090b12dc}.wrap{max-width:1100px;margin:auto}.top{display:flex;justify-content:space-between;align-items:center;gap:14px;flex-wrap:wrap}.brand{display:flex;align-items:center;gap:13px}.logo{width:52px;height:52px;border-radius:15px;background:linear-gradient(135deg,var(--accent),var(--blue));display:grid;place-items:center;font-weight:900;font-size:19px}.eyebrow{font-size:12px;letter-spacing:.1em;color:#c4b5fd;font-weight:800}h1{margin:0;font-size:clamp(24px,4vw,36px);letter-spacing:-.04em}header p{color:var(--muted);max-width:700px;margin:14px 0 0}
main{padding:24px 18px 48px}.toolbar{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:18px}.toolbar input,.toolbar select,.field{background:#111624;border:1px solid var(--line);color:var(--text);border-radius:10px;padding:12px;font:inherit}.toolbar input{flex:1;min-width:180px}.btn{display:inline-flex;align-items:center;justify-content:center;background:linear-gradient(135deg,var(--accent),#536dfe);border:0;border-radius:10px;color:white;text-decoration:none;font-weight:750;padding:11px 14px;cursor:pointer;font:inherit}.btn.secondary{background:#242b40;border:1px solid #39415c}.btn:disabled{opacity:.45;cursor:not-allowed}.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(225px,1fr));gap:15px}.card{background:linear-gradient(180deg,#171d2c,#111520);border:1px solid var(--line);border-radius:16px;overflow:hidden;display:flex;flex-direction:column;min-height:300px}.cover{height:135px;background:linear-gradient(135deg,#332064,#1b2b5a);display:grid;place-items:center;overflow:hidden}.cover img{width:100%;height:100%;object-fit:cover}.cover .placeholder{font-size:38px;font-weight:900;color:#d8ccff}.body{padding:16px;display:flex;flex-direction:column;flex:1}.tag{font-size:11px;text-transform:uppercase;letter-spacing:.08em;color:#c4b5fd;font-weight:800}.card h2{font-size:19px;margin:7px 0 5px}.card p{color:var(--muted);margin:0 0 14px;flex:1;overflow-wrap:anywhere}.meta{font-size:12px;color:#8992aa;margin-bottom:12px}.card .btn{width:100%}.notice{margin-top:22px;padding:15px;border:1px solid #4b426e;background:#17132a;border-radius:12px;color:#ddd6ff}.empty{color:var(--muted);padding:20px}.admin{margin-top:30px;border:1px solid var(--line);border-radius:16px;background:#111624;padding:18px}.admin h2{margin-top:0}.formgrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:11px}.field{width:100%;margin-top:5px}.fieldlabel{display:block;font-size:13px;color:var(--muted)}textarea.field{min-height:84px;resize:vertical}.actions{display:flex;gap:10px;flex-wrap:wrap;margin-top:12px}.hidden{display:none}.admin-note{font-size:13px;color:var(--muted)}.foot{color:#828ba2;font-size:13px;text-align:center;padding:22px;border-top:1px solid var(--line)}
</style>
</head>
<body>
<header><div class="wrap">
  <div class="top">
    <div class="brand"><div class="logo">MDM</div><div><h1>MDM PKG Store</h1><div class="eyebrow">HOMEBREW • PS4 • GOLDHEN</div></div></div>
    <button class="btn secondary" id="toggleAdmin">Painel de administração</button>
  </div>
  <p>Catálogo de homebrew, utilitários e emuladores para PS4. Pesquise aplicativos e baixe arquivos disponibilizados pelo administrador.</p>
</div></header>
<main class="wrap">
  <div class="toolbar">
    <input id="search" type="search" placeholder="Buscar aplicativo..." aria-label="Buscar aplicativo">
    <select id="category" aria-label="Filtrar categoria"><option value="all">Todas as categorias</option></select>
  </div>
  <div id="grid" class="grid" aria-live="polite"></div>
  <div class="notice"><strong>Importante:</strong> esta loja não vem com jogos comerciais, canais pagos ou arquivos de terceiros. Use apenas PKGs que você criou ou tem autorização para distribuir. Os links de download precisam estar hospedados em um serviço acessível.</div>

  <section class="admin hidden" id="admin">
    <h2>Painel de administração</h2>
    <p class="admin-note">Adicione itens ao catálogo, incluindo URL do PKG e imagem de capa. Esta versão salva os dados neste navegador e permite exportar/importar o catálogo. Para que as alterações apareçam para todos os visitantes, será necessário publicar o catálogo atualizado ou conectar um backend.</p>
    <form id="appForm">
      <div class="formgrid">
        <label class="fieldlabel">Nome do aplicativo<input class="field" id="name" required placeholder="Ex.: Meu Homebrew"></label>
        <label class="fieldlabel">Categoria<select class="field" id="appCategory"><option>Homebrew</option><option>Utilitários</option><option>Emuladores</option><option>Multimídia</option><option>Outros</option></select></label>
        <label class="fieldlabel">Versão<input class="field" id="version" placeholder="Ex.: 1.0"></label>
        <label class="fieldlabel">URL direta do PKG<input class="field" id="url" type="url" placeholder="https://.../arquivo.pkg"></label>
        <label class="fieldlabel">URL da imagem de capa<input class="field" id="image" type="url" placeholder="https://.../capa.jpg"></label>
      </div>
      <label class="fieldlabel" style="margin-top:11px">Descrição<textarea class="field" id="description" placeholder="O que o aplicativo faz?"></textarea></label>
      <div class="actions"><button class="btn" type="submit">Adicionar aplicativo</button><button class="btn secondary" type="button" id="export">Exportar catálogo JSON</button><button class="btn secondary" type="button" id="importBtn">Importar catálogo JSON</button><input id="importFile" type="file" accept="application/json,.json" class="hidden"></div>
    </form>
    <p id="status" class="admin-note" aria-live="polite"></p>
    <h3>Itens adicionados neste navegador</h3><div id="manageList"></div>
  </section>
</main>
<footer class="foot">MDM PKG Store • Projeto independente • Catálogo de downloads autorizados.</footer>
<script>
const seed=[
 {id:"demo-homebrew",name:"Homebrew de exemplo",category:"Homebrew",version:"—",description:"Exemplo de cadastro. Substitua pelos dados do seu aplicativo.",url:"",image:""},
 {id:"demo-utils",name:"Utilitário de exemplo",category:"Utilitários",version:"—",description:"Adicione ferramentas compatíveis que você tem autorização para distribuir.",url:"",image:""},
 {id:"demo-emulator",name:"Emulador de exemplo",category:"Emuladores",version:"—",description:"Cadastre um emulador homebrew e informe sua licença e compatibilidade.",url:"",image:""}
];
const KEY="mdm-pkg-store-catalog-v1";
let apps=seed;
try{const saved=JSON.parse(localStorage.getItem(KEY)||"null");if(Array.isArray(saved))apps=saved}catch(e){}
const $=s=>document.querySelector(s), grid=$("#grid"), search=$("#search"), category=$("#category"), status=$("#status");
function save(){try{localStorage.setItem(KEY,JSON.stringify(apps));status.textContent="Catálogo salvo neste navegador."}catch(e){status.textContent="Não foi possível salvar localmente. Exporte o catálogo JSON."}}
function safeUrl(value){try{const u=new URL(value);return ["https:","http:"].includes(u.protocol)?u.href:""}catch(e){return ""}}
function render(){const q=search.value.trim().toLowerCase(),cat=category.value;const cats=[...new Set(apps.map(a=>a.category).filter(Boolean))].sort();const old=cat;category.innerHTML='<option value="all">Todas as categorias</option>';cats.forEach(c=>{const o=document.createElement("option");o.value=c;o.textContent=c;category.append(o)});category.value=cats.includes(old)?old:"all";const list=apps.filter(a=>(category.value==="all"||a.category===category.value)&&(`${a.name} ${a.category} ${a.description}`.toLowerCase().includes(q)));grid.replaceChildren();if(!list.length){grid.innerHTML='<div class="empty">Nenhum aplicativo encontrado.</div>';return}list.forEach(a=>{const card=document.createElement("article");card.className="card";const cover=document.createElement("div");cover.className="cover";if(safeUrl(a.image)){const img=document.createElement("img");img.src=safeUrl(a.image);img.alt="Capa de "+a.name;img.loading="lazy";img.onerror=()=>{cover.replaceChildren();const ph=document.createElement("div");ph.className="placeholder";ph.textContent="MDM";cover.append(ph)};cover.append(img)}else{const ph=document.createElement("div");ph.className="placeholder";ph.textContent="MDM";cover.append(ph)}const body=document.createElement("div");body.className="body";const tag=document.createElement("div");tag.className="tag";tag.textContent=a.category||"Outros";const h=document.createElement("h2");h.textContent=a.name;const p=document.createElement("p");p.textContent=a.description||"Sem descrição.";const meta=document.createElement("div");meta.className="meta";meta.textContent="Versão: "+(a.version||"—");const link=document.createElement("a");link.className="btn";const url=safeUrl(a.url);if(url){link.href=url;link.target="_blank";link.rel="noopener noreferrer";link.textContent="Baixar PKG"}else{link.textContent="Link não configurado";link.classList.add("disabled");link.href="#";link.addEventListener("click",e=>e.preventDefault())}body.append(tag,h,p,meta,link);card.append(cover,body);grid.append(card)});renderManage()}
function renderManage(){const box=$("#manageList");box.replaceChildren();apps.forEach((a,i)=>{const row=document.createElement("div");row.style.cssText="display:flex;justify-content:space-between;gap:10px;align-items:center;padding:9px 0;border-top:1px solid #2a3044";const t=document.createElement("span");t.textContent=a.name+" — "+a.category;const b=document.createElement("button");b.className="btn secondary";b.textContent="Excluir";b.type="button";b.addEventListener("click",()=>{apps.splice(i,1);save();render()});row.append(t,b);box.append(row)})}
$("#toggleAdmin").addEventListener("click",()=>$("#admin").classList.toggle("hidden"));
$("#appForm").addEventListener("submit",e=>{e.preventDefault();const item={id:"app-"+Date.now(),name:$("#name").value.trim(),category:$("#appCategory").value,version:$("#version").value.trim()||"—",description:$("#description").value.trim(),url:safeUrl($("#url").value.trim()),image:safeUrl($("#image").value.trim())};if(!item.name){status.textContent="Informe o nome do aplicativo.";return}apps.push(item);save();e.target.reset();render();status.textContent="Aplicativo adicionado. Exporte o JSON para guardar uma cópia."});
$("#export").addEventListener("click",()=>{const blob=new Blob([JSON.stringify(apps,null,2)],{type:"application/json"});const a=document.createElement("a");a.href=URL.createObjectURL(blob);a.download="mdm-pkg-catalog.json";a.click();URL.revokeObjectURL(a.href);status.textContent="Catálogo exportado. Guarde o arquivo JSON."});
$("#importBtn").addEventListener("click",()=>$("#importFile").click());
$("#importFile").addEventListener("change",async e=>{const f=e.target.files[0];if(!f)return;try{const parsed=JSON.parse(await f.text());if(!Array.isArray(parsed)||parsed.some(x=>!x||typeof x.name!=="string"))throw Error("Formato inválido");apps=parsed.map((a,i)=>({id:String(a.id||"import-"+i),name:String(a.name),category:String(a.category||"Outros"),version:String(a.version||"—"),description:String(a.description||""),url:safeUrl(String(a.url||"")),image:safeUrl(String(a.image||""))}));save();render();status.textContent="Catálogo importado com sucesso."}catch(err){status.textContent="Não foi possível importar: confira se o JSON é válido."}e.target.value=""});
search.addEventListener("input",render);category.addEventListener("change",render);render();
</script>
</body>
</html>