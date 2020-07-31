<template>
    <div id="menu">
        <label for="tm" id="toggle-menu">CMC Corporation<span class="drop-icon">▾</span></label>
        <input type="checkbox" id="tm">
        <ul class="main-menu clearfix">
            <li><img src="@/assets/logo.png" alt="CMC Logo" id="nav-logo"></li>
            <li><a href="#">Home</a></li>
            <li><a href="#">About
                <span class="drop-icon">▾</span>
                <label title="Toggle Drop-down" class="drop-icon" for="sm1">▾</label>
            </a>
                <input type="checkbox" id="sm1">
                <ul class="sub-menu">
                    <li><a href="#">CMC Corp</a></li>
                    <li><a href="#">Members
                        <span class="drop-icon">▾</span>
                        <label title="Toggle Drop-down" class="drop-icon" for="sm2">▾</label>
                    </a>
                        <input type="checkbox" id="sm2">
                        <ul class="sub-menu">
                            <li><a href="#">CMC Global</a></li>
                            <li><a href="#">CMC Telecom</a></li>
                            <li><a href="#">CMC TS</a></li>
                        </ul>
                    </li>
                    <li><a href="#">Leaders</a></li>
                </ul>
            </li>
            <li><a href="#">Contact</a>
            </li>
        </ul>
    </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
#nav-logo {
    display: none;
}

#menu {
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 1;
}

#menu ul {
    margin: 0;
    padding: 0;
}

#menu .main-menu {
    display: none;
}

#menu .main-menu img {
    max-width: 25%;
    max-height: 25%;
}

#tm:checked + .main-menu {
    display: block;
}

#menu input[type="checkbox"],
#menu ul span.drop-icon {
    display: none;
}

#menu li,
#toggle-menu,
#menu .sub-menu {
    border-style: solid;
    border-color: rgba(0, 0, 0, 0.05);
}

#menu li,
#toggle-menu {
    border-width: 0 0 1px;
}

#menu .sub-menu {
    background-color: #040f16;
    border-width: 1px 1px 0;
    margin: 0 1em;
}

#menu .sub-menu li:last-child {
    border-width: 0;
}

#menu li,
#toggle-menu,
#menu a {
    position: relative;
    display: block;
    color: white;
    text-shadow: 1px 1px 0 rgba(0, 0, 0, 0.125);
}

#menu,
#toggle-menu {
    background-color: #44475c;
}

#toggle-menu,
#menu a {
    padding: 1em 1.5em;
}

#menu a {
    transition: all 0.125s ease-in-out;
    -webkit-transition: all 0.125s ease-in-out;
}

#menu a:hover {
    background-color: white;
    color: #0094c6;
}

#menu .sub-menu {
    display: none;
}

#menu input[type="checkbox"]:checked + .sub-menu {
    display: block;
}

#menu .sub-menu a:hover {
    color: #444;
}

#toggle-menu .drop-icon,
#menu li label.drop-icon {
    position: absolute;
    right: 1.5em;
    top: 1.25em;
}

#menu label.drop-icon,
#toggle-menu span.drop-icon {
    border-radius: 50%;
    width: 1em;
    height: 1em;
    text-align: center;
    background-color: rgba(0, 0, 0, 0.125);
    text-shadow: 0 0 0 transparent;
    color: rgba(255, 255, 255, 0.75);
}

#menu .drop-icon {
    line-height: 1;
}

</style>