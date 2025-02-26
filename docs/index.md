# Welcome!

???+ success "🎉 恭喜! 现在你是一位 Linux 用户了!"
    <!-- A minimal structure for the ScreenAdapter defined in browser/screen.js -->
    <div id="screen_container" style="display: flex;">
        <div style="white-space: pre; font: 14px monospace; line-height: 14px; margin: auto;"></div>
        <canvas style="display: none"></canvas>
    </div>

    这是使用 [copy/v86](https://github.com/copy/v86) 项目运行的 [Linux](https://en.wikipedia.org/wiki/Linux) 6.8.12 内核, 使用 [Web Assembly](https://webassembly.org/) 技术在你的浏览器上运行了一个虚拟机, 并启动了极简的 [Buildroot](https://buildroot.org/) 环境.
        
    你可以在这里尝试 Linux 常用的命令, 例如 `ls`, `cd`, `cat`, `echo`, `pwd`, `uname`, `date`, `top`, `ps`, `clear`, `exit`.

    注: 如果无法显示，请尝试多刷新几次本页面.

<script src="/notes/javascripts/v86/libv86.js"></script>
<script>
"use strict";

// Save references to the original event handler methods
const originalAddEventListener = window.addEventListener;
const originalRemoveEventListener = window.removeEventListener;

// Array to store keydown listeners
const keydownListeners = [];

// Override addEventListener to track keydown listeners
window.addEventListener = function(type, listener, options) {
originalAddEventListener.call(window, type, listener, options);
if (type === 'keydown') {
    keydownListeners.push({ listener, options });
}
};

// Override removeEventListener to update the keydown listeners list
window.removeEventListener = function(type, listener, options) {
originalRemoveEventListener.call(window, type, listener, options);
if (type === 'keydown') {
    const index = keydownListeners.findIndex(entry => 
    entry.listener === listener && 
    (entry.options === options || 
    (typeof entry.options === 'object' && typeof options === 'object' && 
        JSON.stringify(entry.options) === JSON.stringify(options))));
    if (index !== -1) {
    keydownListeners.splice(index, 1);
    }
}
};

window.onload = function()
{
    // Remove key listener from material mkdocs
    if (keydownListeners.length > 0) {
        const firstListener = keydownListeners.shift();
        window.removeEventListener('keydown', firstListener.listener, firstListener.options);
    }

    var emulator = new V86({
        wasm_path: "/notes/javascripts/v86/v86.wasm",
        memory_size: 512 * 1024 * 1024,
        vga_memory_size: 8 * 1024 * 1024,
        screen_container: document.getElementById("screen_container"),
        bios: {
            url: "/notes/javascripts/v86/seabios.bin",
        },
        vga_bios: {
            url: "/notes/javascripts/v86/vgabios.bin",
        },
        bzimage: {
            url: "/notes/javascripts/v86/buildroot-bzimage68.bin",
        },
        autostart: true,
    });
};
</script>