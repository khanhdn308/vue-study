<template>
    <Menu :source="menu" />
</template>

<script>
import Menu from 'vue-nested-menu'
export default {
    name: "SideMenu",
    components: {
        Menu,
    },
    data() {
        return {
            menu: {
                title: 'CMC Corporation',
                children: [
                    {
                        title: 'About us',
                        link: '/about',
                        children: [],
                    },
                    {
                        title: 'Products',
                        link: '/product',
                        children: [
                            {
                                title: 'Technology & Solution',
                                link: '/tech',
                                children: [],
                            },
                            {
                                title: 'Business',
                                link: '/business',
                                children: [],
                            },
                            {
                                title: 'Research & Development',
                                link: '/rd',
                                children: [],
                            }
                        ]
                    }
                ]
            },
        };
    },
};
</script>