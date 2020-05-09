---
title: ObjectId 的最小实现
date: 2020-02-09 21:17:51
tags:
---

``` js
import { randomBytes } from 'crypto'

let increaser = Math.trunc(Math.random() * 0xffffff)
const PROCESS_UNIQUE = randomBytes(5)

class ObjectId {
  constructor(id) {
    if (!id) {
      this.id = ObjectId.generate(Math.trunc(Date.now() / 1000))
    } else if (typeof id === 'string' && id.length === 24) {
      this.id = Buffer.from(id, 'hex')
    } else if (typeof id === 'number') {
      this.id = ObjectId.generate(id)
    } else if ((Buffer.isBuffer(id) || Array.isArray(id)) && id.length === 12) {
      this.id = Buffer.from(id)
    } else {
      throw new TypeError(
        'Argument passed in must be a single String of 12 bytes or a string of 24 hex characters'
      )
    }
  }

  static generate(timestamp) {
    // https://nodejs.org/zh-cn/docs/guides/buffer-constructor-deprecation/
    // const buffer = Buffer.allocUnsafe(12)
    const buffer = Buffer.alloc(12)
    const counter = increaser++

    // 4-byte timestamp
    buffer[3] = timestamp & 0xff
    buffer[2] = (timestamp >> 8) & 0xff
    buffer[1] = (timestamp >> 16) & 0xff
    buffer[0] = (timestamp >> 24) & 0xff

    // 5-byte process unique
    buffer[4] = PROCESS_UNIQUE[0]
    buffer[5] = PROCESS_UNIQUE[1]
    buffer[6] = PROCESS_UNIQUE[2]
    buffer[7] = PROCESS_UNIQUE[3]
    buffer[8] = PROCESS_UNIQUE[4]

    // 3-byte counter
    buffer[11] = counter & 0xff
    buffer[10] = (counter >> 8) & 0xff
    buffer[9] = (counter >> 16) & 0xff

    return buffer
  }

  getTimestamp() {
    return new Date(this.id.readUInt32BE(0) * 1000)
  }

  toString() {
    return this.id.toString('hex')
  }

  toJson() {
    return this.toString()
  }
}
```
