<!--
    Copyright (c) 2017, German Neuroinformatics Node (G-Node)

    All rights reserved.

    Redistribution and use in source and binary forms, with or without
    modification, are permitted under the terms of the BSD License. See
    LICENSE file in the root of the Project.
-->

<template>
    <div class="container">
        <!-- If a static file has been provided, display content from this file instead of the default gin content -->
        <div v-if="content" v-html="content"></div>

        <!-- default gin content -->
        <div v-if="!content">
            <h2>Imprint</h2>
            <hr/><br/>

            <p>Verantwortlicher gemäß §6 TDG</p><br/>
            <dl class="dl-horizontal">
                <dd>Dr. Thomas Wachtler-Kulla</dd>
                <dd>Biozentrum</dd>
                <dd>Ludwig-Maximilians-Universität München</dd>
                <dd>Großhaderner Straße 2</dd>
                <dd>82152 Martinsried-Planegg</dd>
                <dd>Germany</dd>
            </dl>
            <br/>
            <dl class="dl-horizontal">
                <dt>Phone</dt>
                <dd>+49 (0)89 2180 74810</dd>
                <dt>Fax</dt>
                <dd>+49 89 2180 74803</dd>
                <dt>eMail</dt>
                <dd>wachtler at bio.lmu.de</dd>
            </dl>
            <br/>
            Inhaltlich Verantwortlicher gemäß §10 Absatz 3 MDStV<br/>
            Dr. Thomas Wachtler-Kulla (Anschrift wie oben)<br />
            <br/>
            <h3>Haftungshinweis</h3>
            <p>Trotz sorgfältiger inhaltlicher Kontrolle Übernehmen wir keine Haftung für
            die Inhalte externer Links. Für den Inhalt der verlinkten Seiten sind
            ausschließlich deren Betreiber verantwortlich.</p>
        </div>
    </div>
</template>

<script>
    const ll = "[Info/Imprint]"

    export default {
        data() {
            return {
                content: ""
            }
        },

        mounted() {
            window.log.print("Debug", `${ll} mounting...`)

            const stat_cont = window.api.config.static_content
            const cont_url = window.api.config.static_content.imprint

            if (stat_cont !== undefined && stat_cont !== null && cont_url !== undefined && cont_url !== "") {
                window.log.print("Debug", `${ll} get static file content from ${cont_url}`)
                const f = window.api.getStaticFile(cont_url)
                f.then(
                        (c) => {
                            this.content = c
                        },
                        (error) => {
                            window.log.print("Err", `${ll} error fetching static content`)
                            window.log.print("Err", error)
                        }
                )
            }
        }
    }
</script>
