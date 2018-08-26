<template>
    <div>
        <h2>Adress Information</h2>
        <table id="location-info" cellpadding="5">
            <thead>
                <tr>
                    <th>Address</th>
                    <th>City</th>
                    <th>State</th>
                    <th>Zipcode</th>
                    <th>fips</th>
                    <th>lat</th>
                    <th>lon</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>{{data.address_info.address}}</td>
                    <td>{{data.address_info.city}}</td>
                    <td>{{data.address_info.state}}</td>
                    <td>{{data.address_info.zipcode}}</td>
                    <td>{{data.address_info.county_fips}}</td>
                    <td>{{data.address_info.lat}}</td>
                    <td>{{data.address_info.lng}}</td>
                </tr>
            </tbody>
        </table>
        <h2>Property Information</h2>
        <table id="property-info" cellpadding="5">
            <tr v-bind:key="key" v-for="(value, key ) in data['property/details'].result.property">
                <th >
                    {{key.replace(new RegExp("_", "g")," ")}}
                </th>
                <td>
                    {{value == null ? 'No data' : value}}
                </td>
            </tr>
        </table>
        <h2>Assesment Information</h2>
        <table id="assessment" cellpadding="5">
            <tr v-bind:key="key" v-for="(value, key ) in data['property/details'].result.assessment">
                <th >
                    {{key.replace(new RegExp("_", "g")," ")}}
                </th>
                <td>
                    {{processCommas(value, key)}}
                </td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        name: 'Tables',
        props: {
            data: Object
        },
        methods: {
            processCommas(value, key){
                let res = '';
                if(value == null){
                    res = 'No data';
                }else if(key === 'tax_amount' || key === 'total_assessed_value'){
                        res = Number(value).toLocaleString();
                }else{
                    res = value
                }
                return res;
            }
        }
    }
</script>
<style>
    #location-info{
        margin-top: 20px;
        margin-bottom: 20px;
    }
    #assessment{
        margin-top: 20px;
        margin-bottom: 20px;
    }
    table {
        margin-left : auto;
        margin-right : auto;
        border-collapse:separate;
    }

    table, th, td {
        border: 1px solid black;
    }
</style>