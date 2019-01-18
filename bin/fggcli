#!/usr/bin/env node

/**
 * Module dependencies.
 */

const program = require('commander')
const fs = require('fs')
const path = require('path')

/**
 * Constant
 * @private
 */
const PATH_GLOBAL = path.resolve('./node/global')
const PATH_BASE = path.resolve('./node/base')
const PATH_VUE = path.resolve('./node/vue')

/**
 * Main function
 * @public
 */
program
.version('0.1.0', '-V, --version')
.option('-b, --base', 'Base Node Application')
.option('-v, --vue', 'Node + Vue Application')
.parse(process.argv)

if (program.base) {
    generateBase()
} else if (program.vue) {
    generateVue()
} else {
    console.log('-h, --help')
    console.log('-b, --base', 'Base Node Application')
    console.log('-v, --vue', 'Node + Vue Application')
}

/**
 * Generate Node base project
 * @private
 */
function generateBase () {
    console.log('You are building a Node project')
    copyFilesToRoot(PATH_GLOBAL)
    copyFilesToRoot(PATH_BASE)
}

/**
 * Generate Node + Vue project
 * @private
 */
function generateVue () {
    console.log('You are building a Vue + Node project')
    copyFilesToRoot(PATH_GLOBAL)
    copyFilesToRoot(PATH_VUE)
}

/**
 * Copy all files in directory to projcet root
 * @param {Path} dir
 */
function copyFilesToRoot (dir) {
    const projectRootPath = process.NODE_ENV === 'test'
        ? '../test'
        : __dirname

    getFileList(dir).forEach(file => {
        copyFile(
            path.resolve(dir, file),
            path.resolve(projectRootPath, file)
        )
    })
}

/**
 * Copy a file from src to dest
 * @private
 * @param {Path} src
 * @param {Path} dest
 */
function copyFile (src, dest) {
    const readStream = fs.createReadStream(src)

    readStream.once('error', (err) => {
        console.log(err)
    })

    readStream.once('end', () => {
        console.log('generating:', dest)
    })

    readStream.pipe(fs.createWriteStream(dest))
}

/**
 * Get files names in directory
 * @param {Path} directory
 */
function getFileList (directory) {
    return fs.readdirSync(directory)
}
