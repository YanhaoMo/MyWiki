# .vimrc

```vim
set nocompatible
filetype off
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

"插件管理器
Bundle 'Vundle/Vundle.vim'
"括号等的自动补全
Bundle 'Raimondi/delimitMate'
"文件管理器
Bundle 'Scrooloose/nerdtree'
"文件搜索
Bundle 'Shougo/unite.vim'
"代码结构浏览
Bundle 'majutsushi/tagbar'
"显示git修改状态
Bundle 'airblade/vim-gitgutter'
"gruvbox主题
Bundle 'morhetz/gruvbox'
"不同层次括号着色
Bundle 'kien/rainbow_parentheses.vim'
"状态条增强
Bundle 'bling/vim-airline'
"区块选择增强
Bundle 'tpope/vim-surround'
"快速注释
Bundle 'scrooloose/nerdcommenter'
"快速移动
Bundle 'Lokaltog/vim-easymotion'
"tumux支持
Bundle 'benmills/vimux'
"MarkDown支持
Bundle 'plasticboy/vim-markdown'
"对齐功能增强
Bundle 'junegunn/vim-easy-align'
"浏览最近访问文件
Bundle 'vim-scripts/mru.vim'
"启动界面增强
Bundle 'mhinz/vim-startify'
"多光标编辑
Bundle 'terryma/vim-multiple-cursors'
"语法高亮增强
Bundle 'sheerun/vim-polyglot'
Bundle 'othree/javascript-libraries-syntax.vim'
"PyMode
Bundle 'klen/python-mode'
"Javascript增强
Bundle 'pangloss/vim-javascript'
"补全插件
"Bundle 'Valloric/YouCompleteMe'
"补全增强
"Bundle 'SirVer/ultisnips'
"代码片段支持
"Bundle 'honza/vim-snippets'
"文件搜索
"Bundle 'kien/ctrlp.vim'
"静态语法检查
"Bundle 'scrooloose/syntastic'
"git支持
"Bundle 'tpope/vim-fugitive'

call vundle#end()
filetype plugin indent on

source ~/.vim/config
```

# .vim/config

``` vim
"gvim配置
if has("gui_running")
    let $LANG='en'                                              "设置gvim菜单栏始终显示为英文
    set langmenu=en
    source $VIMRUNTIME/delmenu.vim
    source $VIMRUNTIME/menu.vim
    "set guifont=DejaVu\ Sans\ Mono\ for\ Powerline\ Book\ 10
    "set guifont=DejaVu\ Sans\ Mono\ Book\ 10
    set guifont=Droid\ Sans\ Mono\ Book\ 10
    set guioptions-=e
    set guioptions-=m
    set guioptions-=T
    set guioptions-=L
    set guioptions-=r
    set guioptions-=B
    set guioptions-=0
    set go=
    winpos 1000 0
    "set lines=100 columns=150                                   "开启时的窗口默认大小
endif

syntax on                                                       "语法高亮支持
set nu                                                          "显示行号
set rnu                                                         "显示相对行号
set wrap                                                        "当一行文字很长时换行
set showmatch                                                   "当光标移动到一个括号时会高亮显示对应的另一个括号
set showcmd                                                     "回显输入的命令
set showmode                                                    "显示当前的模式
set clipboard+=unnamed                                          "关联系统的剪贴板
set ruler                                                       "在编辑过程中右下角显示光标的行列信息
set nocp                                                        "让Vim工作在不兼容模式下
set encoding=utf-8                                              "默认使用utf-8编码格式
set shortmess=atI                                               "启动时不显示捐助乌干达儿童的提示
set so=6                                                        "上下滚行时空余6行
set autoindent                                                  "自动套用上一行的缩进方式
set smartindent                                                 "智能缩进
set mouse=a                                                     "开启鼠标支持
set laststatus=2                                                "总是显示状态行
set backspace=indent,eol,start                                  "对退格键提供更好的支持
set ts=4                                                        "设置tab长度为4
set sts=4                                                       "设置制表符宽度
set shiftwidth=4                                                "设置缩进空格数
set expandtab                                                   "用空格代替tab键
set smarttab                                                    "更加智能的tab键
set hid                                                         "当buffer被丢弃时隐藏它
set encoding=utf-8                                              "设置默认编码方式
set fileencodings=utf-8,cp936,gb18030,big5,euc-kr,latin1        "自动判断编码时 依次尝试一下编码
set ffs=unix,dos,mac                                            "设置文件类型
set hlsearch                                                    "高亮搜索内容
set ignorecase                                                  "搜索模式里忽略大小写
set smartcase                                                   "如果搜索字符串里包含大写字母，则禁用 ignorecase
set incsearch                                                   "显示搜索的动态匹配效果
set lazyredraw                                                  "解决某些类型的文件由于syntax导致vim反应过慢的问题
set ttyfast
set cc=130
set foldmethod=indent                                           "折叠方式
set nofoldenable                                                "不自动折叠
set completeopt-=preview                                        "不显示预览窗口
set foldcolumn=1                                                "在行号前空出一列的宽度
set t_Co=256                                                    "设置256真彩色
set cm=blowfish2                                                "使用blowfish2加密算法
"set nowrap                                                     "当一行文字很长时取消换行
"set history=100                                                "设置历史记录条数
"set autoread                                                   "当文件在外部被修改时自动载入
"set cindent                                                    "使用c语言的缩进格式
"set whichwrap+=<,>,h,l                                         "允许backspace和光标键跨越行边界
"set cmdheight=2                                                "显示两行命令行

"设置vim主题外观
colorscheme desert                                              "设置desert高亮主题
"set background=light                                           "设置vim背景为浅色
set background=dark                                             "设置vim背景为深色
set cursorline                                                  "突出显示当前行
"set cursorcolumn                                               "突出显示当前列

set list lcs=tab:\┊\ ,trail:•                                   "显示tab键为┊，并且显示每行结尾的空格为'•'
"一些备用字符:›┆┇┊┋♠♦•
"我的状态行显示的内容
set statusline=[%t]\ %y\ %m%=%{&fileencoding}\ [%{&ff}]\ [%l,\ %c]\ [%L]\ [%p%%]

"备份设置
"set nobackup                                                   "不进行备份
"set nowb                                                       "重新载入文件时不要备份
"set noswapfile                                                 "不使用swf文件，可能导致错误无法恢复

"关闭错误声音
set noerrorbells
set novisualbell
set  t_vb=

"打开一个文件自动定位到上一次退出的位置
if has("autocmd")
    au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif
endif
"保存.vim文件后不用退出即可生效
"au! bufwritepost .vimrc source %

"设置vim主题外观
colorscheme gruvbox                                             "设置gruvbox高亮主题
"set cursorline                                                  "突出显示当前行
"set cursorcolumn                                                "突出显示当前列

"hi CursorLine cterm=NONE ctermbg=237 ctermfg=NONE
"hi CursorColumn cterm=NONE ctermbg=237 ctermfg=NONE

hi vertsplit ctermbg=bg guibg=bg
hi GitGutterAdd ctermbg=bg guibg=bg
hi GitGutterChange ctermbg=bg guibg=bg
hi GitGutterDelete ctermbg=bg guibg=bg
hi GitGutterChangeDelete ctermbg=bg guibg=bg
hi SyntasticErrorSign ctermbg=bg guibg=bg
hi SyntasticWarningSign ctermbg=bg guibg=bg
hi FoldColumn ctermbg=bg guibg=bg

"NERDTree插件配置
let NERDTreeChDirMode=2                                         "设置当前目录为nerdtree的起始目录
let NERDChristmasTree=1                                         "使得窗口有更好看的效果
let NERDTreeMouseMode=1                                         "双击鼠标左键打开文件
let NERDTreeWinSize=35                                          "设置窗口宽度为20
let NERDTreeQuitOnOpen=1                                        "打开一个文件时nerdtree分栏自动关闭
let NERDTreeShowBookmarks=1                                     "默认显示书签

"ctags插件配置
set tags+=/usr/include/tags

"cscope插件配置
if has("cscope")
    "set csprg=/usr/bin/cscope
    set csto=0
    set cst
    set nocsverb
    set cscopequickfix=s-,c-,d-,i-,t-,e- "在quickfix窗口中显示搜索结果


    " add any database in current directory
    if filereadable("cscope.out")
        cs add cscope.out
        " else add database pointed to by environment
    elseif $CSCOPE_DB != ""
        cs add $CSCOPE_DB
    endif
    set csverb
endif

"syntastic插件配置
set statusline+=%#warningmsg#
set statusline+=%{SyntasticStatuslineFlag()}
set statusline+=%*
let g:syntastic_always_populate_loc_list = 1
let g:syntastic_auto_loc_list = 1
let g:syntastic_check_on_open = 1
let g:syntastic_check_on_wq = 1
let g:syntastic_error_symbol = '✗'
let g:syntastic_warning_symbol = '⚡'
"let g:syntastic_cpp_include_dirs = ['/usr/include/qt']
"let g:syntastic_cpp_compiler_options = '-std=gnu++11 -Wall'
let g:syntastic_mode_map = { 'mode': 'passive', 'active_filetypes': [],'passive_filetypes': [] }

"youcompleteme自动补全配置
"let g:loaded_youcompleteme=1
let g:ycm_seed_identifiers_with_syntax=1
let g:ycm_collect_identifiers_from_tags_files=1
let g:ycm_error_symbol = '✗'
let g:ycm_warning_symbol = '⚡'
let g:ycm_add_preview_to_completeopt = 1                "不显示预览窗口
let g:ycm_autoclose_preview_window_after_insertion = 1
let g:ycm_autoclose_preview_window_after_completion = 1
let g:ycm_key_list_select_completion = ['<c-n>', '<Down>', '<CR>']
let g:ycm_key_list_previous_completion = ['<c-p>', '<Up>']
let g:ycm_semantic_triggers = {
            \ 'c' : ['->', '.', ' ', '(', '[', '&'],
            \ 'objc' : ['->', '.'],
            \ 'ocalml' : ['.', '#'],
            \ 'cpp,objcpp' : ['->', '.', ' ', '(', '[', '&', '::'],
            \ 'perl' : ['->', '::'],
            \ 'php' : ['->', '::', '.'],
            \ 'cs,java,javascript,d,python,perl6,scala,vb,elixir,go' : ['.'],
            \ 'vim' : ['re![_a-zA-Z]+[_\w]*\.'],
            \ 'ruby' : ['.', '::'],
            \ 'lua' : ['.', ':'],
            \ 'erlang' : ['.', ':']
            \ }
map <leader>g  :YcmCompleter GoToDefinitionElseDeclaration<CR>

"UltiSnips插件配置
let g:UltiSnipsExpandTrigger="<tab>"
""let g:UltiSnipsJumpForwardTrigger="<tab>"
""let g:UltiSnipsJumpBackwardTrigger="<s-tab>"
let g:UltiSnipsEditSplit = "vertical"
"let g:UltiSnipsSnippetDirectories = ["UltiSnips", "bundle/snippets"]
let g:UltiSnipsSnippetDirectories = ["bundle/snippets"]

"rainbow_parentheses插件配置
let g:rbpt_colorpairs = [
            \ ['brown',       'RoyalBlue3'],
            \ ['Darkblue',    'SeaGreen3'],
            \ ['darkgray',    'DarkOrchid3'],
            \ ['darkgreen',   'firebrick3'],
            \ ['darkcyan',    'RoyalBlue3'],
            \ ['darkred',     'SeaGreen3'],
            \ ['darkmagenta', 'DarkOrchid3'],
            \ ['brown',       'firebrick3'],
            \ ['gray',        'RoyalBlue3'],
            \ ['black',       'SeaGreen3'],
            \ ['darkred',     'DarkOrchid3'],
            \ ['darkmagenta', 'DarkOrchid3'],
            \ ['Darkblue',    'firebrick3'],
            \ ['darkgreen',   'RoyalBlue3'],
            \ ['darkcyan',    'SeaGreen3'],
            \ ['red',         'firebrick3'],
            \ ]
let g:rbpt_max = 16
let g:rbpt_loadcmd_toggle = 0
au VimEnter * RainbowParenthesesToggle
au Syntax * RainbowParenthesesLoadRound
au Syntax * RainbowParenthesesLoadSquare
au Syntax * RainbowParenthesesLoadBraces

"vim-multiple-cursors插件配置
let g:multi_cursor_use_default_mapping=0
let g:multi_cursor_next_key='<C-m>'
let g:multi_cursor_prev_key='<C-p>'
let g:multi_cursor_skip_key='<C-x>'
let g:multi_cursor_quit_key='<Esc>'

"airline插件配置
let g:airline_powerline_fonts=1                                 "配置airline使用powerline字体

"vimwiki插件配置
"let g:vimwiki_list = [{'path' : '~/.vimwiki/',
"        \'template_path' : '~/.vimwiki/template/',
"        \'template_default' : 'default_template',
"        \'template_ext' : '.html',
"        \'path_html': '~/.vimwiki/html/'}
"        \]

"mru插件配置
let MRU_Auto_Close = 1
let MRU_Max_Entries = 40

"Pymode 配置
let g:pymode_rope = 0
let g:pymode_lint_cwindow = 0
let g:pymode_run_bind = '<leader>h'

let g:multi_cursor_next_key='<C-l>'

"设置以空格打开和关闭折叠
nmap <space> @=((foldclosed(line('.'))<0)?'zc':'zo')<CR>
"当一行很长时把分开的段行当作一行来移动
map j gj
map k gk
"将Esc键映射到jj
im jj <Esc>
im JJ <Esc>
im zz <Esc>
map zz <Esc>
im ZZ <Esc>
map ZZ <Esc>
"quickfix相关的一些快捷键
map cop :copen<CR>
map ccl :cclose<CR>
map cn :cn<CR>
map cp :cp<CR>
"emacs式的行内跳转
map <c-a> ^
map <c-e> $
imap <c-a> <Esc>^i
imap <c-e> <Esc>$a
"ff跳转到文件末尾
map ff G
"visual模式下快速对齐
vnoremap < <gv
vnoremap > >gv

map <F4> :!ctags -R --c++-kinds=+p --fields=+iaS --extra=+q .<CR>
im <F4> <Esc>:!ctags -R --c++-kinds=+p --fields=+iaS --extra=+q .<CR>
nmap go g<C-]>
nmap bk <C-t>

nmap <C-_>s :cs find s <C-R>=expand("<cword>")<CR><CR>
nmap <C-_>g :cs find g <C-R>=expand("<cword>")<CR><CR>
nmap <C-_>c :cs find c <C-R>=expand("<cword>")<CR><CR>
nmap <C-_>t :cs find t <C-R>=expand("<cword>")<CR><CR>
nmap <C-_>e :cs find e <C-R>=expand("<cword>")<CR><CR>
nmap <C-_>f :cs find f <C-R>=expand("<cfile>")<CR><CR>
nmap <C-_>i :cs find i ^<C-R>=expand("<cfile>")<CR>$<CR>
nmap <C-_>d :cs find d <C-R>=expand("<cword>")<CR><CR>

"<F5>更新cscope文件
map <F5> :!cscope -Rbq<CR>
im <F5> <Esc>:!cscope -Rbq<CR>

map <F6> :SyntasticCheck<CR>
im <F6> <Esc>:SyntasticCheck<CR>

"修改<leader>的键盘映射
nmap , <leader>
"当按下\+Enter时取消搜索高亮
map <silent> <leader><CR> :noh<CR>
"Unite插件配置
map <Leader>b :Unite -winheight=10 buffer<CR>
map <Leader>r :MRU<CR>
map <leader>f :NERDTreeToggle<CR>
"Tagbar插件配置
let g:tagbar_autoclose=1
map <leader>t :TagbarToggle<CR>
"设置文件类型辅助
map <leader>s :setfiletype 
"更方便的窗口间跳转
map <leader>j <c-w>j
map <leader>k <c-w>k
map <leader>l <c-w>l
map <leader>h <c-w>h
map <C-j> <c-w>j
map <C-k> <c-w>k
map <C-l> <c-w>l
map <C-h> <c-w>h
"vimux插件配置
map <Leader>e :VimuxPromptCommand<CR>
map <Leader>x :VimuxCloseRunner<CR>
map <Leader>vl :VimuxRunLastCommand<CR>
map <Leader>vi :VimuxInspectRunner<CR>
"更方便的页滚动
map <C-j> <C-f>
map <C-k> <C-b>

map ,,j <Plug>(easymotion-w)
map ,,k <Plug>(easymotion-b)
map ,,s <Plug>(easymotion-s)
```